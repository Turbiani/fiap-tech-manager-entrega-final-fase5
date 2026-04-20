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
O que aconteceu entre a requisição e a resposta é **invisível**. Não há como provar que o cadastro foi criado, o morador contactado e a autorização explicitamente concedida.

---

## Decisão

Adotamos **Event-Driven Architecture com padrão Saga Orquestrado**.

### Cadeia de eventos — Branch A (visitante existente)
```
VISITOR_PRESENTED → VISUAL_CHECK_PASSED → VISITOR_LOOKUP_COMPLETED →
AUTHORIZATION_REQUESTED → AUTHORIZATION_GRANTED → ACCESS_GRANTED
```

### Cadeia de eventos — Branch B (visitante novo)
```
VISITOR_PRESENTED → VISUAL_CHECK_PASSED → VISITOR_LOOKUP_COMPLETED →
VISITOR_REGISTERED → AUTHORIZATION_REQUESTED → AUTHORIZATION_GRANTED → ACCESS_GRANTED
```

O evento `VISITOR_REGISTERED` foi adicionado para fechar o Gap crítico do Risco 1 e Risco 2:
o TC exige prova de que o cadastro foi **criado**, não apenas consultado.

### Detecção de Coação — Dois Vetores

O TC descreve dois cenários distintos que exigem mecanismos diferentes:

**Vetor A — Pressão no Totem (lado do visitante):**
Coercion Engine no Edge analisa o áudio: palavras-chave, hesitação vocal, score composto.
Emite `COERCION_RISK_DETECTED` silenciosamente.

**Vetor B — Coação do Morador internamente (lado do app):**
O TC diz: *"morador legítimo possa estar sob ameaça — a simples confirmação de identidade deixa de ser indicador confiável."* Para este cenário:

- **Panic Code Silencioso:** segurar o botão de autorização por 3s ou usar PIN alternativo gera `COERCION_SILENT_ALARM` sem bloquear o acesso — para não escalar a ameaça.
- **Anomalia Comportamental:** velocidade de resposta atípica, geolocalização incomum, padrão de toque diferente do baseline histórico.

```json
{
  "event_type": "COERCION_SILENT_ALARM",
  "trigger": "panic_hold | panic_pin | behavioral_anomaly",
  "access_request_id": "uuid",
  "morador_id": "uuid",
  "response_time_ms": 450,
  "dispatched_to": ["operator", "siem"]
}
```

---

## Alternativas Consideradas

| Alternativa | Motivo de Rejeição |
|-------------|-------------------|
| **REST síncrono** | Não garante rastro de etapas intermediárias |
| **Banco compartilhado** | Acoplamento forte; dificulta escala independente |
| **Saga coreografada** | Difícil garantir sequência obrigatória de etapas |

---

## Consequências

### Positivas ✅
- Rastro completo de cada etapa — Risco 1 e Risco 2 fechados
- `VISITOR_REGISTERED` comprova criação de cadastro (gap original corrigido)
- Dois vetores de coação cobertos — Risco 4 fechado
- Extensível: novos consumidores adicionados sem alterar o fluxo principal
- Retry automático via Dead Letter Queue

### Negativas / Trade-offs ⚠️
- Consistência eventual (não imediata)
- Complexidade operacional maior que REST simples
- Monitoramento de consumer lag obrigatório
- Idempotência obrigatória em todos os consumidores

---

## Critério de Revisão

Reavaliar para **Apache Kafka** se volume superar 10.000 eventos/hora por condomínio.
