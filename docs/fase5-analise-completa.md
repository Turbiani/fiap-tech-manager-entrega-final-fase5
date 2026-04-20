# 🎓 Fase 5 — Enterprise Architecture & Liderança
## Análise Completa: Tech Challenge × Disciplinas × Proposta SmartGate

> **Projeto:** SmartGate — Segurança Condominial Inteligente  
> **Curso:** PosTech FIAP — 2TCMT | Grupo 18  
> **Responsável por esta análise:** Leonardo Turbiani — RM366050  
> **Foco particular:** Seção 3 — Arquitetura do Software (Alto Nível)

---

## 📍 Parte 1 — Tech Challenge × Disciplinas da Fase 5

> **Como ler esta seção:** cada entregável do TC é mapeado às disciplinas que o sustentam teoricamente. Serve como guia de estudo e checklist de coerência na proposta.

### 1.1 Mapa de Cobertura

| Entregável do Tech Challenge | Disciplinas que sustentam | Aulas relevantes |
|---|---|---|
| **Visão Geral da Solução Digital** | Advanced Leadership Skills | Aula 1 — Motivação 4.0 (protagonismo e propósito) |
| **Arquitetura do Software (Alto Nível)** | Observabilidade | Aulas 1–4 — Do monitoramento à visão estratégica |
| **Arquitetura do Software (Alto Nível)** | Gestão da Mudança em TI | Aula 2 — RFC e ADR (decisões arquiteturais documentadas) |
| **Funcionalidades dos Módulos** | Gestão das Equipes e Retenção | Aula 3 — Autonomia e empowerment (squads por pilar) |
| **Casos de Uso com IA** | Estratégia Cloud & FinOps | Aulas 2, 3 — Multi-cloud, Well-Architected, edge + cloud |
| **Jornadas de Usuário** | Cultura Organizacional | Aulas 1–2 — DNA cultural, adoção de novas práticas |
| **Stack de Desenvolvimento** | Observabilidade | Aula 2 — Ferramentas de observabilidade (ELK, Prometheus) |
| **Plano de Implementação (Roadmap)** | Gestão da Mudança em TI | Aulas 1, 3, 4 — Gestão da mudança, times adaptáveis, gestão tática |
| **ROI e Métricas Financeiras** | Estratégia Cloud & FinOps | Aula 4 — FinOps by Design; Aula 5 — Pricing model |
| **OKRs e Métricas de Valor** | Gestão das Equipes e Retenção | Aula 1 — Gestão de resultados: do BSC ao OKR |
| **Gestão de Mudança (seção 8.8)** | Gestão da Mudança em TI | Aulas 1, 5 — Gestão da mudança; Gestão do Conhecimento e do Erro |
| **Pitch Deck (opcional)** | Advanced Leadership Skills | Aula 2 — Mindful Leadership (presença e comunicação executiva) |
| **Estrutura de Times (Squads)** | Gestão das Equipes e Retenção | Aulas 2, 3, 4 — Feedback, autonomia, cultura de aprendizado |
| **Conformidade LGPD / Governança** | Estratégia Cloud & FinOps | Aula 3 — Well-Architected e Segurança |
| **Cultura de Adoção da Solução** | Cultura Organizacional | Aulas 3, 4 — Culture Hacking; Times de tecnologia |

---

### 1.2 Status dos PDFs por Disciplina

| Disciplina | Status no Projeto | Prioridade de Ação |
|---|---|---|
| Estratégia Cloud & FinOps e GreenOps | ✅ Aulas 1–5 presentes | Priorizar Aulas 3 e 4 para embasar ROI e stack |
| Gestão das Equipes e Retenção | ✅ Aulas 1–4 presentes | Usar Aula 1 (OKR) e Aula 3 (Autonomia/Squads) |
| Gestão da Mudança em TI | ✅ Aulas 1–5 presentes | Usar Aulas 1 e 2 (RFC/ADR) e Aula 5 (Conhecimento) |
| Advanced Leadership Skills | ✅ Aulas 1–2 (parcial) | Verificar Aulas 3 e 4 — podem estar desatualizadas |
| **Observabilidade** | ❌ Nenhuma aula | **URGENTE — ligado diretamente à stack de monitoramento** |
| **Cultura Organizacional** | ❌ Nenhuma aula | **URGENTE — ligado diretamente à adoção da solução** |
| Tech Challenge Fase 5 | ✅ Adicionado | Briefing oficial do desafio |
| Proposta SmartGate | ✅ Adicionada | Documento de trabalho do grupo |

---

## 📋 Parte 2 — Resumo Completo do Tech Challenge

### 2.1 Contexto do Problema

Uma empresa de **portaria eletrônica** gerencia **20 condomínios residenciais de alto padrão** em São Paulo (até 20 unidades cada). A operação combina:

- **Acesso autônomo:** reconhecimento facial sem intervenção humana
- **Acesso assistido:** operador remoto valida e libera manualmente

O desafio foca **exclusivamente nas entradas assistidas**, onde a dependência humana cria vulnerabilidades estruturais.

**Volume operacional:**
- ~40 entradas assistidas por condomínio/dia
- Picos: manhã (7h–10h) com empregados/prestadores e noite de sexta/sábado
- 4 operadores para cada 10 condomínios

**Limitação central:** embora o fluxo seja formalmente definido, não existem mecanismos que garantam sua execução rigorosa nem evidências que comprovem cada etapa.

---

### 2.2 Os 4 Riscos Críticos

| # | Risco | Descrição | Consequência |
|---|---|---|---|
| 1 | **Falta de Garantia de Processo** | Nenhum mecanismo garante que o operador percorra todas as etapas (verificação → cadastro → confirmação) | Etapas críticas puladas silenciosamente, sem alertas |
| 2 | **Ausência de Evidências Auditáveis** | O sistema registra apenas o evento final (liberação), sem comprovar que cada etapa foi cumprida | Impossível investigar, comprovar conformidade ou responsabilizar |
| 3 | **Falta de Controle Visual Sistêmico** | A regra "sem capacete" depende 100% do julgamento humano — sem detecção técnica | Aplicação inconsistente das regras de segurança |
| 4 | **Vulnerabilidade a Coação/Pressão** | Moradores sob ameaça podem autorizar acessos ilegítimos — o sistema não detecta coação | Falha de segurança nos cenários de maior risco |

---

### 2.3 A Missão

Propor um produto ou serviço digital que elimine esses riscos através de:

- **Automação inteligente** de processos críticos
- **Evidências auditáveis** que comprovem conformidade em cada etapa
- **Detecção de anomalias** e situações de risco em tempo real
- **Eficiência operacional** mantida mesmo em picos
- **Escalabilidade** sem crescimento proporcional de equipe

**Restrições do TC:**
- Sem atrito excessivo nem aumento do tempo de atendimento
- Deve funcionar em empresa estabelecida (não é greenfield)
- Implementação faseada (curto, médio, longo prazo)
- Integração com tecnologias existentes

---

### 2.4 Entregáveis

| Entregável | Obrigatoriedade | Conteúdo esperado |
|---|---|---|
| **Documento de Proposta Estratégica (PDF)** | ✅ Obrigatório | Visão geral, arquitetura, módulos, casos de uso com IA, jornadas, stack, roadmap, OKRs |
| **Vídeo de ~10 minutos** (YouTube/Vimeo) | ✅ Obrigatório | Apresentação da solução com link inserido no documento |
| **Pitch Day Online (5 min)** | ⚠️ Recomendado | Apresentação executiva para a diretoria com fator WOW |
| **Protótipo ou Mockup UI** | 💡 Fortemente recomendado | Interface ou demonstração de um módulo-chave |

---

### 2.5 Critérios de Avaliação

| Critério | O que avaliam |
|---|---|
| Compreensão do Problema | A solução resolve os 4 riscos de forma eficaz e abrangente? |
| Inovação e Criatividade | IA integrada de forma genuína e transformadora (não cosmética)? |
| Viabilidade e Pragmatismo | Funciona em empresa real? Roadmap crível? Gestão de mudança considerada? |
| Impacto da IA e Tecnologias Exponenciais | Uso claro, relevante e com potencial de transformação demonstrado? |
| Qualidade do Design e Documentação | Arquitetura, jornadas e plano comunicados com clareza e lógica? |

---

## 🔍 Parte 3 — Avaliação da Proposta SmartGate

> **Escala:** ✅ Forte | ⚠️ Parcial / Oportunidade | ❌ Ausente / Crítico

---

### 3.1 Visão Geral e Enquadramento do Problema (Seções 1–2)

**Avaliação: ✅ Forte**

- Mapeia diretamente os 4 riscos do TC
- Objetivo central bem articulado: "controlar o processo, não apenas a entrada"
- A metáfora do "hub central de governança de acessos" é poderosa e coerente

**Oportunidade:** citar dados reais de mercado sobre incidentes condominiais por falha humana tornaria o problema mais urgente no pitch.

---

### 3.2 Arquitetura do Software — Seção 3 ⭐ (Responsabilidade do Leo)

**Avaliação: ⚠️ Boa base, com lacunas significativas**

**O que está bem:**
- 6 camadas corretamente identificadas e nomeadas
- Princípio **offline-first** é arquiteturalmente sólido e bem justificado para segurança crítica
- Separação edge × cloud reflete entendimento real de latência vs. escala

**Lacunas críticas:**

| Lacuna | Impacto | Recomendação |
|---|---|---|
| **Sem diagrama de arquitetura** | 🔴 Alto — TC pede "alto nível" explicitamente | Criar C4 Level 1 (Contexto) + Level 2 (Containers) |
| **Sem justificativas arquiteturais** | 🟡 Médio — avaliadores esperam o "por quê" | Documentar 2–3 decisões no estilo ADR simplificado |
| **Protocolo de comunicação Edge↔Cloud não especificado** | 🟡 Médio — "como" é tão importante quanto "o quê" | Especificar: MQTT (IoT), REST/gRPC (APIs), fila (SQS) para sync assíncrono |
| **Padrões arquiteturais não citados** | 🟡 Médio | Citar: Event-Driven, CQRS para auditoria, Saga para fluxos críticos |
| **Tratamento de falha não detalhado** | 🔴 Alto para sistema de segurança | Definir: o que acontece se Edge perder conexão? Se reconhecimento facial falhar 3x? |

**Recomendação prática para a Seção 3:**

Transforme a listagem de componentes em uma **narrativa arquitetural** com:

1. **Diagrama C4 Level 1** — SmartGate no contexto: moradores, visitantes, operadores, condomínios, cloud providers
2. **Diagrama C4 Level 2** — Containers: App Mobile, API Gateway, Motor de Decisão, Edge Node, Message Broker, Audit DB, Cloud Sync
3. **3 ADRs simplificados** (apêndice ou seção adicional):
   - ADR-001: Offline-first no Edge vs. cloud-first
   - ADR-002: Arquitetura orientada a eventos vs. request-response síncrono
   - ADR-003: CQRS para a camada de auditoria (separar escrita de leitura)

---

### 3.3 Módulos e Funcionalidades (Seção 4)

**Avaliação: ✅ Forte**

Os 6 pilares cobrem sistematicamente os 4 riscos:

| Risco do TC | Pilar que endereça |
|---|---|
| Risco 1 — Garantia de processo | Pilar 3 — Motor de Decisão + Orquestração de Fluxos |
| Risco 2 — Evidências auditáveis | Pilar 6 — Auditoria, Compliance e Governança |
| Risco 3 — Controle visual | Pilar 5 — Monitoramento Inteligente + Detecção de Anomalias |
| Risco 4 — Coação/pressão | Pilar 3 — Detecção de palavras-chave suspeitas via voz (parcial) |

**Oportunidade:** o Risco 4 está tratado superficialmente. Detalhar o mecanismo de detecção de coação (análise de hesitação vocal + padrão de autorização atípico + horário incomum) seria o diferencial "WOW" do pitch.

---

### 3.4 IA e Tecnologias Exponenciais (Seção 5)

**Avaliação: ✅ Forte**

- YOLO para detecção em tempo real — tecnicamente defensável
- Edge-first para IA (NVIDIA Jetson) — diferencial real de latência e LGPD
- LangChain + LLM para NLP — moderno e flexível
- **Limitação técnica honestamente declarada** (rastreamento contínuo vs. pontos de controle) — demonstra maturidade arquitetural

**Oportunidade:** adicionar uma estratégia básica de **MLOps** — como os modelos de IA são treinados, versionados e monitorados ao longo do tempo. O TC avalia impacto sustentável da IA.

---

### 3.5 Jornadas de Usuário (Seção 6)

**Avaliação: ✅ Forte**

Cobre 6 perfis com fluxos principais e de exceção. Destaques:
- Jornada do Operador como "exceção com máximo contexto" — alinha perfeitamente ao TC
- Jornada de Monitoramento Pós-Acesso é um diferencial que poucos grupos incluirão

---

### 3.6 Stack de Desenvolvimento (Seção 7)

**Avaliação: ✅ Forte com uma ressalva**

| Camada | Escolha | Aderência |
|---|---|---|
| Backend | NestJS | ✅ Modular, enterprise, real-time |
| BD Principal | PostgreSQL | ✅ Consistência forte — crítico para auditoria |
| Cache | Redis | ✅ Latência sub-ms para validação de acesso |
| Mobile | Flutter | ✅ Cross-platform, UX moderna |
| Auth/Push | Firebase | ✅ Biometria integrada + notificações |
| Visão Computacional | YOLO + OpenCV | ✅ Tempo real, edge-friendly |
| Edge | NVIDIA Jetson | ✅ GPU embarcada, offline-first |
| IoT | MQTT (Mosquitto) | ✅ Protocolo leve, padrão de mercado |
| Cloud | AWS | ✅ Maturidade enterprise, arquitetura híbrida |
| Orquestração | Docker + Kubernetes | ✅ Escalabilidade automática |
| Observabilidade | ELK + Prometheus + Grafana | ✅ Stack completa de monitoramento |
| Segurança/Auditoria | JWT + OAuth2 + ELK | ✅ Conformidade LGPD |

**Ressalva:** "OpenClaw" para STT **não é uma tecnologia conhecida no mercado**. A referência correta é **Whisper** (OpenAI, open-source). Avaliadores vão questionar — corrigir antes da entrega.

---

### 3.7 Plano de Implementação e ROI (Seção 8)

**Avaliação: ✅ Muito Forte**

- ROI baseado em dados reais e verificáveis
- 3 cenários financeiros (conservador, moderado, agressivo) demonstram maturidade
- Payback entre 1 e 5 anos — crível
- Roadmap em 3 fases alinhado ao princípio de implementação incremental do TC

**Oportunidade:** a seção de Gestão de Mudança (8.8) é correta mas genérica. Referenciá-la às disciplinas de Cultura Organizacional e Gestão de Mudança em TI da Fase 5 fortaleceria a cobertura acadêmica.

---

### 3.8 OKRs e Métricas (Seção 9)

**Avaliação: ✅ Forte**

| OKR | Risco do TC endereçado |
|---|---|
| OKR 1 — Automatização (85%→95% por fase) | Risco 1 — Garantia de processo |
| OKR 2 — Rastreabilidade (100% auditável) | Risco 2 — Evidências auditáveis |
| OKR 3 — Experiência (NPS ≥70, ≤30s autorização) | Restrição do TC (sem atrito) |
| OKR 4 — Detecção de Anomalias (≥80%, <10% falso positivo) | Risco 3 — Controle visual |
| OKR 5 — Conformidade LGPD (100%) | Requisito de governança |

---

### 3.9 Gaps Consolidados

| Item | Impacto | Responsável | Ação |
|---|---|---|---|
| **Diagrama de arquitetura** (C4 L1+L2) | 🔴 Crítico | Leo | Criar e inserir na Seção 3 |
| **ADRs ou decisões arquiteturais** | 🟡 Médio | Leo | Documentar 2–3 decisões-chave |
| **Protocolo Edge↔Cloud detalhado** | 🟡 Médio | Leo | Especificar MQTT + fila + sync assíncrono |
| **Detalhamento anti-coação** | 🟡 Médio (WOW) | Grupo | Especificar mecanismo composto |
| **Estratégia MLOps** | 🟡 Médio | Grupo | Como modelos evoluem e são monitorados? |
| **Link do vídeo de 10 min** | 🔴 Obrigatório | Grupo | Gravar, publicar e inserir link no PDF |
| **Mockup de interface** | 🟡 Recomendado | Grupo | App do morador + painel do operador |
| **Correção "OpenClaw → Whisper"** | 🟡 Baixo mas visível | Grupo | Corrigir nomenclatura antes da entrega |

---

## 🎯 Scorecard Final

| Critério do TC | Nota Estimada | Comentário |
|---|---|---|
| Compreensão do Problema | 9/10 | Clara e completa; Risco 4 poderia ser mais detalhado |
| Inovação e Criatividade | 8/10 | Edge-first + offline-first são diferenciais genuínos |
| Viabilidade e Pragmatismo | 9/10 | ROI sólido, roadmap crível, limitações honestamente declaradas |
| Impacto da IA | 8/10 | Bom uso pragmático; falta MLOps e evolução dos modelos |
| Qualidade do Design e Doc. | 7/10 | **Falta o diagrama de arquitetura — gap mais crítico** |
| **Média estimada** | **8,2/10** | Proposta sólida com gaps pontuais e solucionáveis |

---

## ✅ Plano de Ação Prioritário

### Leo (Seção 3 — Arquitetura):
1. Criar diagrama **C4 Level 1** — SmartGate no ecossistema
2. Criar diagrama **C4 Level 2** — Containers com tecnologias mapeadas
3. Documentar **3 ADRs** simplificados
4. Detalhar **comunicação Edge↔Cloud**: protocolos, filas, sync offline
5. Descrever **fallback e tratamento de falha** arquitetural

### Grupo (restante):
6. Gravar vídeo de 10 min → publicar no YouTube → inserir link no PDF
7. Criar mockup de 2 telas (app morador + painel operador em exceção)
8. Detalhar mecanismo de detecção de coação (candidato a fator WOW)
9. Corrigir "OpenClaw" → "Whisper (OpenAI open-source)"

### Projeto no Claude (base de conhecimento):
10. Adicionar PDFs de **Observabilidade** (4 aulas)
11. Adicionar PDFs de **Cultura Organizacional** (4 aulas)

---

*Análise gerada como guia de estudo e avaliação — Grupo 18 | PosTech FIAP 2TCMT | Fase 5*
