# ADR-003 — CQRS na Camada de Auditoria

| Campo | Valor |
|-------|-------|
| **Status** | ✅ Aceita |
| **Data** | 2026-03-10 |
| **Autores** | Leonardo Turbiani (RM366050) |
| **Revisores** | Grupo 18 — 2TCMT |
| **Contexto** | Fase 5 — SmartGate · Tech Challenge 2TCMT |

---

## Contexto

A camada de auditoria do SmartGate tem dois requisitos **estruturalmente conflitantes**:

**Requisito Write (Risco 2 do TC):**
- Deve ser **append-only e imutável** — nenhum registro pode ser alterado ou deletado
- Toda tentativa de adulteração deve ser detectável via hash encadeado
- Performance de escrita deve ser máxima (eventos chegam em alta frequência)

**Requisito Read (Compliance e Operação):**
- Relatórios de conformidade com joins e agregações complexas
- Dashboards de operador em tempo real (latência < 50ms)
- Exportação LGPD por titular de dados
- Investigações de incidentes com filtros variados

Usar um único modelo de banco satisfaz mal os dois requisitos:
- Índices para consultas degradam a performance de escrita
- Constraints append-only impedem projeções materializadas eficientes
- Contention em updates de views bloqueia inserts de eventos críticos

---

## Decisão

Adotamos **CQRS (Command Query Responsibility Segregation)** separando completamente Write e Read:

### Write Side — Command (Imutabilidade Garantida)
```sql
-- Enforced via trigger no banco — NUNCA UPDATE ou DELETE
CREATE OR REPLACE FUNCTION prevent_modification()
RETURNS TRIGGER AS $$
BEGIN
  RAISE EXCEPTION 'Audit events are immutable. No UPDATE or DELETE allowed.';
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER audit_immutability
BEFORE UPDATE OR DELETE ON audit_events
FOR EACH ROW EXECUTE FUNCTION prevent_modification();
```
- PostgreSQL com role de banco sem permissão de UPDATE/DELETE
- Hash encadeado SHA-256 (cada evento referencia o hash do anterior)
- Otimizado para INSERT sequencial: sem índices complexos na tabela principal

### Read Side — Query (Projeções Otimizadas)
- PostgreSQL Read Replica com streaming replication (lag ~100ms)
- **Event Processor** projeta views materializadas por caso de uso:

| View | Consumidor | Finalidade |
|------|-----------|-----------|
| `compliance_view` | Admin Portal | Relatórios por condomínio/período |
| `risk_view` | Operator Dashboard | Anomalias e alertas em tempo real |
| `dashboard_view` | Redis Cache | Métricas operacionais (< 50ms) |
| `lgpd_view` | DPO / Exportação | Dados por titular para direitos LGPD |

---

## Alternativas Consideradas

| Alternativa | Motivo de Rejeição |
|-------------|-------------------|
| **Banco único** para leitura e escrita | Performance degradada em ambos os lados; conflito de requisitos |
| **Event Sourcing puro** sem CQRS | Relatórios de compliance extremamente lentos (replay de todos os eventos) |
| **DynamoDB** para auditoria | Sem garantias relacionais para joins de compliance; custo elevado em consultas complexas |
| **Elasticsearch** como único store | Não oferece garantias ACID para o write side; dificulta conformidade LGPD |

---

## Consequências

### Positivas ✅
- Write side permanece intacto — adulteração detectável por hash encadeado
- Read side evolui independentemente sem impactar a auditoria
- Relatórios de compliance com performance < 2s mesmo com anos de histórico
- Conformidade LGPD: exportação por titular via read side sem tocar no write
- Dashboards operacionais em < 50ms via Redis Cache

### Negativas / Trade-offs ⚠️
- Consistência **eventual** entre write e read (~100ms de lag de replicação)
- Duas instâncias de banco para manter e monitorar
- Event Processor deve ser **idempotente** (eventos podem ser reprocessados)
- Maior complexidade de onboarding para novos desenvolvedores

---

## Critério de Revisão

Reavaliar arquitetura se:
- Volume do write side superar 10TB — avaliar particionamento por condomínio
- Necessidade de auditoria em tempo real < 10ms — considerar EventStoreDB
- Requisitos LGPD evoluírem para exigir portabilidade entre clouds
