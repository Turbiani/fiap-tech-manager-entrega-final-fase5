# 🎓 Mapa de Aprendizado — MBA PosTech Tech Management (Fase 4)

> **Projeto:** VittaHub — Sistema de Comunicação Digital de Boletins Médicos
> **Curso:** FIAP/PosTech — Grupo 18 | Fevereiro 2026
> **Objetivo deste documento:** Organizar **todos os 50+ documentos do projeto** em tópicos sequenciais para facilitar o estudo e a conexão entre os temas.

---

## 📍 Como usar este mapa

Cada **Trilha** é uma disciplina do MBA. Dentro de cada trilha, as aulas estão na ordem recomendada. Os ícones indicam o tipo de conteúdo:

- 📄 = Documento markdown/docx do projeto (produzido pelo grupo)
- 📕 = PDF de aula teórica (material do curso)
- 📋 = ADR (Architecture Decision Record)
- 🎯 = Documento do desafio (briefing do Tech Challenge)

---

## 🗺️ Visão Geral — As 10 Trilhas

| # | Trilha | Foco Principal | Qtd. Docs |
|---|--------|---------------|-----------|
| 1 | Arquitetura de Software | Modelos, Clean Architecture, C4, ADRs, Débito Técnico | 13 |
| 2 | Governança de TI | Frameworks, KPIs, tomada de decisão | 4 |
| 3 | Cyber Security & DevSecOps | Segurança, Red/Blue/Purple Team, shift-left | 5 |
| 4 | Dados & Inteligência Artificial | Estratégia de dados, IA como produto, governança | 5 |
| 5 | Estratégia Cloud, FinOps & GreenOps | Cloud, multi-cloud, Well-Architected, custos | 5 |
| 6 | Ecossistemas Digitais & Inovação | Hype Cycle, APIs, Blockchain, IA Generativa | 4 |
| 7 | Gestão de Mudanças em TI | Frameworks de mudança, resistência, adoção | 5 |
| 8 | Liderança & Desenvolvimento Humano | Motivação, mindful leadership, diversidade | 4 |
| 9 | Gestão de Times & Resultados | Resultados, feedback, empowerment, aprendizado | 4 |
| 10 | Projeto VittaHub (Entregáveis) | Documentação produzida pelo grupo | 4 |

---

## 🏗️ TRILHA 1 — Arquitetura de Software

**Conceito-chave:** Tomar decisões arquiteturais proporcionais ao estágio do produto.

Esta trilha é o coração do Entregável 1 da Fase 4. A lógica de estudo é: primeiro entender os modelos existentes, depois analisar o que já temos, decidir o modelo certo, organizar internamente, documentar com C4 e planejar a evolução.

### 1.1 Fundamentos Teóricos (Aulas)

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 1️⃣ | 📕 `Aula_1__Arquiteturas_da_Atualidade.pdf` | **Panorama de modelos arquiteturais:** monólito, microsserviços, hexagonal, onion, clean architecture e seus trade-offs. É a base teórica para todas as decisões do projeto. |
| 2️⃣ | 📕 `Aula_2__Documentação_de_Arquitetura_com_o_Modelo_C4.pdf` | **Modelo C4 (Context, Container, Component, Code):** como documentar arquitetura em níveis progressivos de zoom. Essencial para criar diagramas profissionais. |
| 3️⃣ | 📕 `Aula_3__Requisitos_Funcionais_e_Não_Funcionais_rev2.pdf` | **Requisitos:** como classificar e priorizar requisitos funcionais (o que o sistema faz) e não-funcionais (como o sistema se comporta — performance, segurança, escalabilidade). |
| 4️⃣ | 📕 `Aula_4__Propostas_Arquiteturais_com_RFCs_e_ADRs.pdf` | **RFCs e ADRs:** como documentar decisões arquiteturais de forma formal e rastreável. ADRs registram "o que decidimos, por quê, e quais as consequências". |
| 5️⃣ | 📕 `Aula_5__Gerenciamento_de_Débito_Técnico.pdf` | **Débito técnico:** como identificar, classificar e gerenciar dívidas técnicas conscientes. Analogia: débito técnico é como dívida financeira — pode ser estratégico se for consciente. |

### 1.2 Aplicação Prática (Documentos do Projeto)

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 6️⃣ | 📄 `01-analise-arquitetura-atual.md` | **Diagnóstico AS-IS:** análise honesta da Fase 3, identificando pontos fortes (DDD, ACL, Privacy by Design) e gaps (classificação errada como "microsserviços", falta de camadas formais, observabilidade indefinida). |
| 7️⃣ | 📄 `02-decisao-modelo-arquitetural.md` | **Decisão TO-BE:** comparação entre Monólito Tradicional, Microsserviços e Monólito Modular. Justificativa baseada em critérios concretos (equipe de 5 devs, MVP, 1 hospital). |
| 8️⃣ | 📄 `03-clean-architecture-aplicada.md` | **Organização interna:** as 4 camadas (Entities → Use Cases → Interface Adapters → Frameworks & Drivers) aplicadas ao VittaHub com exemplos em Dart. A regra de dependência é o conceito central. |
| 9️⃣ | 📄 `04-diagramas-c4.md` | **Diagramas C4 (3 níveis):** Context (ecossistema), Container (blocos técnicos) e Component (Clean Architecture visível). O Nível 3 é a principal contribuição da Fase 4. |
| 🔟 | 📄 `05-roadmap-evolucao.md` | **Roadmap em 4 fases:** Monólito Modular → Amadurecido → Híbrido → Microsserviços, cada uma ativada por gatilhos mensuráveis (não por especulação). |

### 1.3 Registros de Decisão (ADRs)

| Documento | Decisão registrada |
|-----------|-------------------|
| 📋 `ADR-001-modelo-monolito-modular.md` | Por que Monólito Modular e não microsserviços |
| 📋 `ADR-002-clean-architecture.md` | Por que Clean Architecture e não Hexagonal/Onion |
| 📋 `ADR-003-estrategia-migracao-futura.md` | Strangler Fig Pattern para migração incremental |

### 💡 Conceitos-chave desta trilha

- **Regra de Dependência:** imports só apontam de fora para dentro (nunca o domínio conhece a infraestrutura)
- **Strangler Fig Pattern:** migração gradual de monólito para microsserviços, extraindo um módulo por vez
- **Evolução por evidência:** cada mudança arquitetural deve ser justificada por um gatilho concreto e mensurável
- **ACL (Anti-Corruption Layer):** isola o sistema legado MV para que mudanças externas não propaguem internamente

---

## 🏛️ TRILHA 2 — Governança de TI

**Conceito-chave:** Alinhar decisões de TI com objetivos de negócio.

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 1️⃣ | 📕 `POSTECH_Governanc_a_em_TI__Aula_1.pdf` | **Fundamentos de governança corporativa e de TI:** diferença entre governança e gestão, 5 domínios de decisão de TI (princípios, arquitetura, infraestrutura, necessidades de aplicação, investimento), papel do Tech Leader. |
| 2️⃣ | 📕 `POSTECH_Governanc_a_em_TI__Aula_2.pdf` | **Frameworks de governança:** COBIT, ITIL, ISO 38500 e como escolher/combinar frameworks para o contexto da organização. |
| 3️⃣ | 📕 `POSTECH_Governança_em_TI__Aula_3.pdf` | **Governança na prática:** implementação de estruturas, comitês, processos de aprovação, SLAs e métricas de desempenho. |
| 4️⃣ | 📕 `POSTECH_Governança_em_TI__Aula_4.pdf` | **Governança avançada:** inovação digital, KPIs dinâmicos com IA, governança ágil para organizações que precisam equilibrar controle e velocidade. |

### 💡 Conceitos-chave desta trilha

- **Governança ≠ Gestão:** Governança define "quem decide o quê"; gestão executa
- **5 Domínios de decisão de TI:** Princípios, Arquitetura, Infraestrutura, Aplicações, Investimento
- **Tech Leader como ponte:** traduz diretrizes estratégicas em ações técnicas operacionais

---

## 🔐 TRILHA 3 — Cyber Security & DevSecOps

**Conceito-chave:** Segurança integrada desde o início (shift-left), não apenas no final.

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 1️⃣ | 📕 `POSTECH__Aula_01_Cyber_Security__O_que_é_importante_para_um_Tech_Lead.pdf` | **Visão do Tech Lead em segurança:** gestão de riscos cibernéticos, frameworks (NIST, ISO 27001, CIS), casos reais (SolarWinds, IA maliciosa), responsabilidades do líder técnico. |
| 2️⃣ | 📕 `POSTECH__Aula_02__Cyber_Security__Red_Team_Blue_Team_Purple_Team.pdf` | **Equipes de segurança:** Red Team (ataque simulado), Blue Team (defesa), Purple Team (colaboração entre ambos). Estratégias de teste de penetração e resposta a incidentes. |
| 3️⃣ | 📕 `POSTECH__Aula_03___Cultura_DevOps_na_organizações.pdf` | **Cultura DevOps:** os 3 caminhos (flow, feedback, aprendizado contínuo), Infrastructure as Code (IaC), IAM em nuvem, desafios culturais da adoção. Cases: Spotify, Netflix, GDS UK. |
| 4️⃣ | 📕 `POSTECH__Aula_04__Técnicas_de_DevSecOps.pdf` | **DevSecOps na prática:** shift-left security, SAST/DAST, pipelines CI/CD seguros, container security, chaos engineering. O "Sec" no meio de DevOps. |
| 5️⃣ | 📕 `POSTECH__Aula_05__Relação_entre_o_DevOps_e_metodologias_ágeis.pdf` | **DevOps + Ágil:** como Scrum, Kanban e DevOps se complementam, métricas DORA (deploy frequency, lead time, MTTR, change failure rate), integração com metodologias ágeis. |

### 💡 Conceitos-chave desta trilha

- **Shift-left:** antecipar segurança para o início do ciclo de desenvolvimento (reduz custo de correção em até 100x)
- **DevSecOps:** segurança como responsabilidade de todos, não de um time separado
- **Chaos Engineering:** testar resiliência derrubando coisas de propósito (Netflix Chaos Monkey)
- **Métricas DORA:** 4 indicadores para medir maturidade de entrega de software

---

## 📊 TRILHA 4 — Dados & Inteligência Artificial

**Conceito-chave:** Dados como ativo estratégico e IA como produto.

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 1️⃣ | 📕 `POSTECH__Aula_1__Fundamentos_de_Dados_e_Estratégia_de_Valor.pdf` | **Fundamentos:** dados como ativo estratégico, cadeia de valor dos dados, Data Mesh vs Data Lake, estratégia data-driven para Tech Managers. |
| 2️⃣ | 📕 `POSTECH__Aula_2__Dados_e_Inteligência_Artificial_Como_Produtos.pdf` | **IA como produto:** product thinking aplicado a dados e modelos de IA, métricas de sucesso, ciclo de vida de produtos de dados. |
| 3️⃣ | 📕 `POSTECH__Aula_3__Engenharia_de_Dados_e_Arquitetura_Escalável.pdf` | **Engenharia de dados:** pipelines ETL/ELT, arquiteturas de ingestão escaláveis, data warehouse vs data lakehouse, ferramentas modernas. |
| 4️⃣ | 📕 `POSTECH__Aula_4__Governança_Compliance_e_Segurança_em_Dados_e_IA.pdf` | **Governança de dados:** LGPD, compliance, vieses em IA, IA responsável, privacidade por design (conecta com o VittaHub). |
| 5️⃣ | 📕 `POSTECH__Aula_5__Inteligencia_Artificial_na_Pratica_e_no_Futuro.pdf` | **IA na prática:** LLMs, IA generativa aplicada, casos de uso reais, limitações e riscos, futuro da IA em organizações. |

### 💡 Conceitos-chave desta trilha

- **Data Mesh:** descentralizar a propriedade dos dados por domínio (alinha com DDD!)
- **LGPD e Privacy by Design:** proteção de dados sensíveis de saúde (diretamente aplicável ao VittaHub)
- **IA Responsável:** vieses, explicabilidade e governança de modelos

---

## ☁️ TRILHA 5 — Estratégia Cloud, FinOps & GreenOps

**Conceito-chave:** Nuvem como estratégia (não apenas infraestrutura), otimizando custo e sustentabilidade.

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 1️⃣ | 📕 `Aula_01__Princípios_benefícios_e_motivadores_da_estratégia_cloud.pdf` | **Fundamentos cloud:** motivadores de migração, CCoE (Cloud Center of Excellence), introdução ao FinOps, metáfora semáforo vs rotatória. |
| 2️⃣ | 📕 `Aula_02__Single_Cloud_Multi_Cloud__Hybrid_Cloud.pdf` | **Modelos de adoção:** single cloud, multi-cloud e hybrid cloud — quando usar cada um, trade-offs de vendor lock-in vs complexidade. |
| 3️⃣ | 📕 `Aula_03__FRAMEWORKS_DE_WELLARCHITECTED_E_SEGURANÇA.pdf` | **Well-Architected Frameworks:** pilares (excelência operacional, segurança, confiabilidade, performance, otimização de custos, sustentabilidade), práticas de segurança em nuvem. |
| 4️⃣ | 📕 `Aula_04__FinOps_by_Design.pdf` | **FinOps:** os 3 pilares (informar, otimizar, operar), maturidade FinOps, impacto da IA nos custos de nuvem, tendências 2025. |
| 5️⃣ | 📕 `Aula_05__Pricing_model_adjustments.pdf` | **Modelos de pricing:** reserved instances, spot, savings plans, GreenOps (sustentabilidade em cloud), como otimizar custos com right-sizing. |

### 💡 Conceitos-chave desta trilha

- **CCoE:** de "semáforo" (TI controlando tudo) para "rotatória" (autonomia com guardrails)
- **FinOps:** unir finanças + engenharia + negócio para otimizar custos de nuvem
- **Well-Architected:** framework para avaliar se sua arquitetura está sólida em 6 pilares

---

## 🌐 TRILHA 6 — Ecossistemas Digitais & Inovação

**Conceito-chave:** Identificar tendências tecnológicas e integrá-las ao produto.

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 1️⃣ | 📕 `Aula_01__Hype_Cycle_Tendências_e_Aplicabilidade.pdf` | **Hype Cycle do Gartner:** como avaliar maturidade de tecnologias (trigger → pico → vale → produtividade), filtrando hype de valor real. |
| 2️⃣ | 📕 `Aula_02__Integrações_e_APIs.pdf` | **APIs e integrações:** API-first design, REST, GraphQL, gRPC, API Gateway, estratégias de versionamento, marketplace de APIs. |
| 3️⃣ | 📕 `Aula03__Open_Data_Blockchain_e_Smart.pdf` | **Blockchain e dados abertos:** Open Data, smart contracts, DeFi, NFTs, aplicações em supply chain e saúde. |
| 4️⃣ | 📕 `Aula_04IA_Generativa_Democratizada_e_Genarative_IA.pdf` | **IA Generativa:** LLMs, Copilot, RAG, fine-tuning, aplicações práticas, riscos de alucinação, impacto em produtos digitais. |

### 💡 Conceitos-chave desta trilha

- **Hype Cycle:** ferramenta para não embarcar em tecnologia por moda, mas por maturidade
- **API-first:** projetar APIs antes da implementação (o VittaHub usa isso com a ACL/MV)
- **IA Generativa para produtos:** possível evolução do VittaHub (simplificação de linguagem médica)

---

## 🔄 TRILHA 7 — Gestão de Mudanças em TI

**Conceito-chave:** Mudanças técnicas só funcionam se as pessoas aceitarem mudar.

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 1️⃣ | 📕 `POSTECH__Gestão_de_Mudança_em_TI__Aula_1.pdf` | **Fundamentos:** por que mudanças falham, modelos de gestão de mudanças (Kotter, ADKAR, Lewin), resistência organizacional. |
| 2️⃣ | 📕 `POSTECH__Gestão_de_Mudanças_em_TI__Aula_2.pdf` | **Planejamento:** como planejar mudanças técnicas (migrações, adoção de novas ferramentas), stakeholder management, comunicação. |
| 3️⃣ | 📕 `POSTECH__Gestão_de_Mudanças_em_TI__Aula_3.pdf` | **Execução:** gerenciando a transição, quick wins, métricas de adoção, gestão de conflitos durante mudanças. |
| 4️⃣ | 📕 `POSTECH__Gestão_de_Mudanças_em_TI__Aula_4.pdf` | **Sustentação:** como institucionalizar mudanças para que não regridam, cultura de melhoria contínua, lições aprendidas. |
| 5️⃣ | 📕 `POSTECH__Gestão_de_Mudanças_em_TI__Aula_5_rev2.pdf` | **Casos e tendências:** mudanças em escala (transformação digital completa), mudanças ágeis, anti-padrões comuns. |

### 💡 Conceitos-chave desta trilha

- **Modelo de Kotter:** 8 passos para liderar mudanças (urgência → coalizão → visão → comunicação → empoderamento → quick wins → consolidação → cultura)
- **ADKAR:** Awareness, Desire, Knowledge, Ability, Reinforcement — focado no indivíduo
- **Aplicação no VittaHub:** migrar de "microsserviços" para "monólito modular" é uma mudança que precisa de buy-in do time

---

## 🧠 TRILHA 8 — Liderança & Desenvolvimento Humano

**Conceito-chave:** Liderança é autenticidade, não estilo.

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 1️⃣ | 📕 `Aula_1__Motivacao_rev2.pdf` | **Motivação:** intrínseca vs extrínseca, Teoria da Autodeterminação (autonomia, competência, vínculo), como motivar equipes técnicas sem depender apenas de bônus. |
| 2️⃣ | 📕 `Aula_2__Mindful_leardeship_rev2.pdf` | **Mindful Leadership:** inteligência emocional (Goleman), autoconsciência, autocontrole, empatia, gestão de relacionamentos, liderança consciente. |
| 3️⃣ | 📕 `Aula_3__Protagonismo_e_autorresponsabilidade_rev2.pdf` | **Protagonismo:** autorresponsabilidade, mindset de crescimento (Carol Dweck), sair da posição de vítima, accountability pessoal e organizacional. |
| 4️⃣ | 📕 `Aula_4__Diversidade_e_inovacao_rev2.pdf` | **Diversidade e inovação:** como times diversos inovam mais, vieses inconscientes, inclusão como estratégia (não apenas compliance), segurança psicológica. |

### 💡 Conceitos-chave desta trilha

- **Motivação 3.0 (Daniel Pink):** autonomia + maestria + propósito > dinheiro para trabalho criativo
- **Growth Mindset (Dweck):** acreditar que habilidades podem ser desenvolvidas (vs. "nasci assim")
- **Segurança psicológica (Amy Edmondson):** ambiente onde errar não gera punição, gerando inovação

---

## 👥 TRILHA 9 — Gestão de Times & Resultados

**Conceito-chave:** Equipes de alta performance são construídas com confiança, feedback e autonomia.

| Ordem | Documento | O que você aprende |
|:---:|-----------|-------------------|
| 1️⃣ | 📕 `POSTECH__Aula_1__Gestão_de_Resultados_rev2.pdf` | **Gestão de resultados:** OKRs, KPIs, métricas de sucesso, como definir e acompanhar indicadores que importam (não "métricas de vaidade"). |
| 2️⃣ | 📕 `POSTECH__Aula_2__11_E_GESTÃO_DE_FEEDBACKS_rev.pdf` | **1:1 e feedback:** reuniões one-on-one eficazes, tipos de feedback (construtivo, reforço), escuta empática, cultura de alto desempenho. |
| 3️⃣ | 📕 `POSTECH__Aula_3__AUTONOMIA_E_EMPOWERMENT_DAS_EQUIPES.pdf` | **Empowerment:** os 4 pilares (poder, motivação, desenvolvimento, liderança), descentralização de decisões, delegação inteligente, segurança psicológica. |
| 4️⃣ | 📕 `POSTECH__Aula_4__IMPLEMENTANDO_Cultura_de_Aprendizado_nos_times.pdf` | **Cultura de aprendizado:** modelo PERMA (psicologia positiva), debriefings, mentoria, mundo BANI, Motivação 3.0 (autonomia, maestria, propósito). |

### 💡 Conceitos-chave desta trilha

- **OKRs:** Objectives (qualitativo, inspirador) + Key Results (quantitativo, mensurável)
- **Feedback ≠ Crítica:** feedback é uma ferramenta de crescimento, não de punição
- **Empowerment:** líder como facilitador que constrói autonomia, não como centralizador

---

## 📦 TRILHA 10 — Projeto VittaHub (Documentos de Entrega)

**Estes são os meta-documentos que contextualizam tudo:**

| Documento | Conteúdo |
|-----------|---------|
| 🎯 `Challenge_Tech_Management__Fase_4.pdf` | **Briefing do desafio:** o que cada entregável pede (arquitetura, governança, dados, DevSecOps, ecossistemas) |
| 📄 `README.md` | **Índice do repositório:** estrutura, links, resumo das decisões, referências bibliográficas |
| 📄 `ArquiteturaVittaHub.docx` | **Documento completo da arquitetura** formatado para entrega |
| 📄 `Tech_Challenge-Fase_3-Grupo_18-TCMT-Jan2026.docx` | **Entrega da Fase 3:** referência do que já foi feito (TOGAF/ADM, DDD, Event Storming, Privacy by Design) |

---

## 🔗 Como os Temas se Conectam

Este diagrama mostra como as trilhas se interligam na prática do VittaHub:

```
                    ┌─────────────────────┐
                    │   🎯 Tech Challenge │
                    │      (Briefing)     │
                    └──────────┬──────────┘
                               │
              ┌────────────────┼────────────────┐
              ▼                ▼                ▼
    ┌─────────────┐  ┌─────────────────┐  ┌──────────────┐
    │ 🏗️ Trilha 1 │  │  🏛️ Trilha 2    │  │ 📊 Trilha 4  │
    │ Arquitetura │  │  Governança TI  │  │ Dados & IA   │
    │             │  │                 │  │              │
    │ Clean Arch  │  │ Decisões de TI  │  │ LGPD/Privacy │
    │ C4 / ADRs   │  │ alinhadas ao    │  │ by Design    │
    │ Roadmap     │  │ negócio         │  │ IA no VittaHub│
    └──────┬──────┘  └────────┬────────┘  └──────┬───────┘
           │                  │                   │
           ▼                  ▼                   ▼
    ┌─────────────┐  ┌─────────────────┐  ┌──────────────┐
    │ 🔐 Trilha 3 │  │  ☁️ Trilha 5    │  │ 🌐 Trilha 6  │
    │ DevSecOps   │←→│  Cloud/FinOps   │  │ Ecossistemas │
    │             │  │                 │  │              │
    │ Segurança   │  │ Infraestrutura  │  │ APIs, IA Gen │
    │ no pipeline │  │ e custos        │  │ Integrações  │
    └──────┬──────┘  └────────┬────────┘  └──────┬───────┘
           │                  │                   │
           └─────────┬────────┘                   │
                     ▼                            │
    ┌─────────────────────────────────────────────┤
    │         TEMAS HUMANOS E ORGANIZACIONAIS     │
    ├─────────────┬───────────────┬────────────────┘
    │ 🔄 Trilha 7 │ 🧠 Trilha 8  │ 👥 Trilha 9
    │ Mudanças    │ Liderança     │ Gestão Times
    │             │               │
    │ Como fazer  │ Quem lidera   │ Como o time
    │ as mudanças │ as mudanças   │ performa
    │ pegarem     │               │
    └─────────────┴───────────────┴───────────────
```

### Conexões práticas mais importantes:

1. **Arquitetura → DevSecOps:** a Clean Architecture facilita testes automatizados (shift-left security)
2. **Arquitetura → Cloud:** o roadmap de evolução (Fase 3/4) implica migração para cloud com API Gateway
3. **Governança → Dados:** governança de TI define quem decide sobre dados e IA
4. **Dados → Arquitetura:** LGPD/Privacy by Design influencia diretamente as Entities do domínio
5. **Ecossistemas → Arquitetura:** a ACL do VittaHub é um caso prático de integração via API
6. **Mudanças → Tudo:** qualquer evolução técnica exige gestão de mudança com as pessoas
7. **Liderança → Times:** cultura de feedback e empowerment sustentam a autonomia técnica

---

## 📌 Sugestão de Roteiro de Estudo

Se você tem **tempo limitado**, siga esta ordem de prioridade:

### Semana 1 — Fundamento Arquitetural (Entregável 1)
1. `Aula_1__Arquiteturas_da_Atualidade.pdf` → base teórica
2. `01-analise-arquitetura-atual.md` → diagnóstico
3. `02-decisao-modelo-arquitetural.md` → decisão
4. `03-clean-architecture-aplicada.md` → organização interna

### Semana 2 — Documentação e Evolução
5. `Aula_2__Documentação_de_Arquitetura_com_o_Modelo_C4.pdf` → como documentar
6. `04-diagramas-c4.md` → diagramas do projeto
7. `Aula_4__Propostas_Arquiteturais_com_RFCs_e_ADRs.pdf` → ADRs
8. `05-roadmap-evolucao.md` → plano de evolução

### Semana 3 — Governança, Cloud e Segurança
9. Governança de TI: Aulas 1-2
10. Cloud e FinOps: Aulas 1, 3, 4
11. Cyber Security: Aulas 1, 4 (DevSecOps)

### Semana 4 — Dados, Ecossistemas e Liderança
12. Dados & IA: Aulas 1-2, 4 (governança LGPD)
13. Ecossistemas: Aulas 1-2
14. Liderança e Times: conforme necessidade para os entregáveis

---

> **Princípio guia do projeto:** *"A maturidade técnica não se mede pela sofisticação das ferramentas, mas pela adequação das escolhas ao contexto real."*
