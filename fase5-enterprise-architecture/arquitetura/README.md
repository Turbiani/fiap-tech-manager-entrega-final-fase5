# Arquitetura do Software — Alto Nível

> **Responsável:** Leonardo Turbiani (RM366050)  
> **Seção do TC:** 3 — Arquitetura do Software (Alto Nível)

## Arquivos

| Arquivo | Descrição |
|---------|-----------|
| [`smartgate-arquitetura-alto-nivel.md`](./smartgate-arquitetura-alto-nivel.md) | Documento completo: C4 L1, C4 L2, Sequence Diagram, CQRS, Stack mapeada, 3 ADRs e tabela de rastreabilidade Arquitetura × Riscos do TC |
| [`smartgate-secao3-diagnostico.md`](./smartgate-secao3-diagnostico.md) | Gap analysis da Seção 3 atual vs. necessária + nota sobre correção OpenClaw → Whisper |

## Diagramas incluídos

- **C4 Level 1** — Contexto do SmartGate no ecossistema
- **C4 Level 2** — Containers e comunicação (Mermaid)
- **Sequence Diagram** — Fluxo de acesso assistido com eventos imutáveis
- **State Diagram** — Resiliência offline (Online → Degraded → Offline → Syncing)
- **CQRS Diagram** — Write Side (append-only) × Read Side (projeções)
