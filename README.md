# 🎓 FIAP PosTech — Tech Management MBA
## Entrega Final — Fase 5: Enterprise Architecture & Liderança

<div align="center">

![PosTech FIAP](https://img.shields.io/badge/PosTech-FIAP-red?style=for-the-badge)
![MBA](https://img.shields.io/badge/MBA-Tech%20Management-blue?style=for-the-badge)
![Fase](https://img.shields.io/badge/Fase-5%20%7C%20Enterprise%20Architecture-purple?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow?style=for-the-badge)

</div>

---

## 👥 Grupo 18 — 2TCMT

| Nome | RM | Responsabilidade |
|------|-----|-----------------|
| Gleiciele Correia de Souza | RM366293 | Gestão de Mudança & Cultura Organizacional |
| Henrique Silva Corrêa | RM366511 | Jornadas de Usuário & Estratégia |
| Igor Cavalcante Montenegro Cerqueira | RM365962 | Módulos Funcionais & IA |
| **Leonardo Turbiani** | **RM366050** | **Arquitetura de Software (Alto Nível)** |
| Regina Lima Garrido | RM365852 | ROI, OKRs & Plano de Implementação |

---

## 🏗️ Sobre o Projeto — SmartGate

> **SmartGate** é uma plataforma digital de governança de acessos condominiais que transforma o controle de portaria de um processo dependente de decisões humanas em um sistema inteligente, automatizado, auditável e escalável.

### O Problema que Resolvemos

Uma empresa de portaria eletrônica que gerencia 20 condomínios em São Paulo enfrenta quatro riscos estruturais:

| # | Risco | Impacto |
|---|-------|---------|
| 1 | **Falta de Garantia de Processo** | Etapas críticas podem ser puladas sem alerta |
| 2 | **Ausência de Evidências Auditáveis** | Impossível comprovar conformidade ou investigar incidentes |
| 3 | **Falta de Controle Visual Sistêmico** | Regras dependem de julgamento humano inconsistente |
| 4 | **Vulnerabilidade a Coação** | Sistema não detecta moradores sob pressão |

### Nossa Resposta

```
Automação inteligente + Evidências imutáveis + IA aplicada + Edge Computing
= Processo controlado, rastreável e resiliente
```

---

## 📁 Estrutura do Repositório

```
fiap-tech-manager-entrega-final-fase5/
│
├── 📄 README.md                          ← Este arquivo
│
├── 📂 fase5-enterprise-architecture/     ← Tech Challenge Fase 5
│   ├── 📂 arquitetura/                   ← Seção 3 — Arquitetura do Software
│   │   ├── smartgate-arquitetura-alto-nivel.md    ← C4, ADRs, Diagramas
│   │   └── smartgate-secao3-diagnostico.md        ← Gap analysis
│   │
│   └── 📂 adrs/                          ← Architecture Decision Records
│       ├── ADR-001-offline-first-edge.md
│       ├── ADR-002-event-driven-architecture.md
│       └── ADR-003-cqrs-auditoria.md
│
├── 📂 fase4-arquitetura-software/        ← Tech Challenge Fase 4
│   ├── 01-analise-arquitetura-atual.md
│   ├── 03-clean-architecture-aplicada.md
│   ├── ADR-002-clean-architecture.md
│   └── ADR-003-estrategia-migracao-futura.md
│
├── 📂 docs/                              ← Documentação de suporte
│   ├── mapa-aprendizado-postech-fase4.md
│   └── fase5-analise-completa.md
│
└── 📂 assets/                            ← Imagens e recursos visuais
```

---

## 🏛️ Arquitetura do Software — Visão Rápida

A arquitetura SmartGate é estruturada em **três boundaries** com comunicação via eventos:

```
┌─────────────────────────────────────────────────────────────────┐
│  EDGE LAYER (Condomínio — NVIDIA Jetson Orin)                   │
│  Camera AI · Audio Module · Edge Orchestrator · Local Store     │
└────────────────────────────┬────────────────────────────────────┘
                             │ MQTT + SQS (async)
┌────────────────────────────▼────────────────────────────────────┐
│  CLOUD LAYER (AWS — São Paulo)                                  │
│  API Gateway · Decision Engine · Audit Service (CQRS)          │
│  Anomaly Detector · Coercion Engine · Message Broker (SQS)     │
└────────────────────────────┬────────────────────────────────────┘
                             │ REST / WebSocket
┌────────────────────────────▼────────────────────────────────────┐
│  PRESENTATION LAYER                                             │
│  Mobile App (Flutter) · Operator Dashboard · Admin Portal      │
└─────────────────────────────────────────────────────────────────┘
```

**3 princípios arquiteturais fundamentais:**
- 🔌 **Offline-First** — falha de conectividade nunca trava a segurança
- 📨 **Event-Driven** — cada etapa gera evidência imutável (Saga Pattern)
- 📋 **CQRS na Auditoria** — escrita append-only separada da leitura

Detalhamento completo em [`fase5-enterprise-architecture/arquitetura/`](./fase5-enterprise-architecture/arquitetura/).

---

## 🔑 Decisões Arquiteturais (ADRs)

| ADR | Decisão | Status |
|-----|---------|--------|
| [ADR-001](./fase5-enterprise-architecture/adrs/ADR-001-offline-first-edge.md) | Arquitetura Offline-First no Edge | ✅ Aceita |
| [ADR-002](./fase5-enterprise-architecture/adrs/ADR-002-event-driven-architecture.md) | Arquitetura Orientada a Eventos (EDA + Saga) | ✅ Aceita |
| [ADR-003](./fase5-enterprise-architecture/adrs/ADR-003-cqrs-auditoria.md) | CQRS na Camada de Auditoria | ✅ Aceita |

---

## 🛠️ Stack Tecnológica Principal

| Camada | Tecnologia |
|--------|-----------|
| Edge AI | Python · YOLO v8 · OpenCV · Whisper (OpenAI) |
| Edge Hardware | NVIDIA Jetson Orin |
| Backend | NestJS · TypeScript |
| Banco de Dados | PostgreSQL · Redis (ElastiCache) |
| Mobile | Flutter (iOS + Android) |
| IoT | MQTT (Mosquitto) |
| Message Broker | AWS SQS + SNS |
| Cloud | AWS (EKS · RDS · S3 · API Gateway) |
| Observabilidade | ELK Stack · Prometheus · Grafana |

---

## 📊 OKRs da Solução

| OKR | Meta Fase 1 | Meta Fase 3 |
|-----|------------|------------|
| Automatização de acessos | ≥ 85% | ≥ 95% |
| Rastreabilidade | 100% auditável | 100% auditável |
| Tempo de autorização | < 30s | < 30s |
| Detecção de anomalias | — | ≥ 80% |
| Conformidade LGPD | 100% | 100% |

---

## 📚 Referências Técnicas

- [C4 Model — Simon Brown](https://c4model.com)
- [ADR — Michael Nygard](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)
- [Saga Pattern — Chris Richardson](https://microservices.io/patterns/data/saga.html)
- [CQRS Pattern — Martin Fowler](https://martinfowler.com/bliki/CQRS.html)
- [Whisper — OpenAI](https://github.com/openai/whisper)

---

## 🎓 Contexto Acadêmico

> **Curso:** MBA Tech Management — PosTech FIAP  
> **Fase:** 5 — Enterprise Architecture & Liderança  
> **Turma:** 2TCMT  
> **Disciplinas cobertas:** Enterprise Architecture · Advanced Leadership Skills · Gestão da Mudança em TI · Observabilidade · Cultura Organizacional · Estratégia Cloud & FinOps

---

<div align="center">
<sub>PosTech FIAP · MBA Tech Management · Grupo 18 · 2TCMT · 2026</sub>
</div>
