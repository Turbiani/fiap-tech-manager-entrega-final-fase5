# ADR-002 — Arquitetura Orientada a Eventos (EDA + Saga Pattern)

| Campo | Valor |
|-------|-------|
| **Status** | ✅ Aceita |
| **Data** | 2026-03-05 |
| **Autores** | Leonardo Turbiani (RM366050) |
| **Revisores** | Grupo 18 — 2TCMT |
| **Contexto** | Fase 5 — SmartGate · Tech Challenge 2TCMT |

---

## Contexto

O problema central do Tech Challenge **não é executar o processo de acesso**, mas **garantir e comprovar que cada etapa foi executada**. O sistema legado registra apenas o evento final (porta aberta), mas não deixa rastro auditável das etapas intermediárias — exatamente os Riscos 1 e 2 do briefing.

Em uma arquitetura **request-response tradicional**:
```
POST /liberar-acesso → { ok: true }
```
O que aconteceu entre a requisição e a resposta é **invisível**. Não há como provar que:
- O cadastro foi consultado
- O morador foi contactado
- A autorização foi explicitamente concedida
- Cada validação foi executada na ordem correta

---

## Decisão

Adotamos **Event-Driven Architecture com padrão Saga Orquestrado** para o fluxo de acesso.

### Princípio
Cada etapa do fluxo é uma **transição de estado explícita** que:
1. Gera um evento imutável publicado no broker (AWS SQS)
2. É persistida no Audit Service antes de avançar
3. Só permite progresso quando o evento anterior for confirmado

### Cadeia obrigatória de eventos
```
VISITOR_PRESENTED
    → VISUAL_CHECK_PASSED (ou VISUAL_CHECK_FAILED → encerra)
        → VISITOR_LOOKUP_COMPLETED
            → AUTHORIZATION_REQUESTED
                → AUTHORIZATION_GRANTED (ou AUTHORIZATION_DENIED → encerra)
                    → ACCESS_GRANTED
```

**Nenhuma etapa pode ser pulada.** O Decision Engine (Saga Orchestrator) valida a sequência antes de emitir o próximo comando. Se um evento não for confirmado dentro do timeout definido, o Saga emite `ACCESS_TIMEOUT` e encerra o fluxo.

### Estrutura de cada evento
```json
{
  "event_id": "uuid-v4",
  "event_type": "AUTHORIZATION_GRANTED",
  "aggregate_id": "access-request-uuid",
  "timestamp": "2026-03-15T08:32:41.123Z",
  "payload": { "morador_id": "...", "biometric_hash": "..." },
  "previous_event_id": "uuid-do-evento-anterior",
  "previous_hash": "sha256(evento_anterior)",
  "current_hash": "sha256(event_id + timestamp + payload + previous_hash)"
}
```

---

## Alternativas Consideradas

| Alternativa | Motivo de Rejeição |
|-------------|-------------------|
| **REST síncrono** | Não garante rastro de etapas intermediárias — resolve só o evento final |
| **Banco compartilhado** entre serviços | Acoplamento forte; dificulta escala e manutenção independente |
| **Saga coreografada** (sem orquestrador) | Difícil garantir sequência obrigatória e detectar etapas puladas |
| **Workflow engine** (Temporal, Conductor) | Overhead excessivo para o escopo atual; pode ser adotado em escala futura |

---

## Consequências

### Positivas ✅
- Rastro completo e imutável de cada etapa (elimina Risco 1 e Risco 2)
- Desacoplamento: Audit Service processa independentemente sem afetar o fluxo
- Extensível: novos consumidores (Anomaly Detector, SIEM) adicionados sem alterar o fluxo principal
- Retry automático via Dead Letter Queue (DLQ) para eventos não processados
- Replay de eventos para investigação de incidentes

### Negativas / Trade-offs ⚠️
- Consistência **eventual** (não imediata) — aceitável para auditoria, não para decisão de acesso
- Complexidade operacional maior que REST simples
- Monitoramento de consumer lag na fila é obrigatório (alerta se lag > threshold)
- Idempotência obrigatória em todos os consumidores

---

## Critério de Revisão

Reavaliar para **Apache Kafka** se:
- Volume superar 10.000 eventos/hora por condomínio
- Necessidade de replay histórico de longo prazo (event sourcing completo)
- Múltiplos sistemas externos precisarem consumir os mesmos eventos
