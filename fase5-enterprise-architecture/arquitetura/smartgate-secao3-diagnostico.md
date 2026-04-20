# Diagnóstico: Seção 3 Atual vs. Seção 3 Necessária

## O que a Seção 3 diz hoje (resumo honesto)

A seção atual tem **6 blocos de texto** descrevendo componentes em formato de lista de funcionalidades.
É tecnicamente correta, mas **não é uma arquitetura de software** — é uma descrição operacional.

| Componente atual | O que diz | O que falta |
|---|---|---|
| 3.1 Backoffice | "cadastro de condomínios, regras, alertas" | Como se conecta ao Edge? Que API? |
| 3.2 Web/Mobile | "criar acessos, notificações, QR Codes" | Mesmo que Seção 4.2 — duplicação |
| 3.3 Edge Computing | "reconhecimento offline, hardware" | Como opera sem internet? Qual protocolo? |
| 3.4 Motor de Decisão | "valida, classifica, determina ação" | Como orquestra? Síncrono ou assíncrono? |
| 3.5 Auditoria | "logs, evidências, histórico" | Como garante imutabilidade? |
| 3.6 Sync Cloud↔Edge | "replicação, offline-first, fila" | Que fila? Que protocolo? Como reconcilia? |

**Problema central:** a Seção 3 responde "O QUÊ" mas o TC pede que ela responda "COMO".

---

## Plano de atualização da Seção 3

O texto atual (320 palavras) pode ser mantido como introdução narrativa.
O que precisa ser ADICIONADO:

### Adição 1 — Diagrama C4 Level 1 (Contexto)
Mostra o SmartGate no ecossistema: usuários, sistemas externos, fluxo de dados.
Responde: "Quem usa e com o que se conecta?"

### Adição 2 — Diagrama C4 Level 2 (Containers)  
Mostra os blocos tecnológicos deployáveis e como se comunicam.
Responde: "Como é construído tecnicamente?"

### Adição 3 — Fluxo de Acesso Assistido (Sequence Diagram)
Mostra cada etapa gerando um evento imutável.
Responde: "Como os 4 riscos são eliminados passo a passo?"

### Adição 4 — Arquitetura de Resiliência Offline
State diagram mostrando Online → Degraded → Offline → Syncing.
Responde: "O que acontece quando a internet cai?"

### Adição 5 — CQRS na Camada de Auditoria
Diagrama separando Write Side (append-only) do Read Side (projeções).
Responde: "Como as evidências são imutáveis?"

### Adição 6 — 3 ADRs
Decisões arquiteturais justificadas com contexto, alternativas e trade-offs.
Responde: "Por que essa arquitetura e não outra?"

---

## Nota sobre "OpenClaw" na Seção 7

O documento usa "OpenClaw" como tecnologia de Speech-to-Text.
**Não existe** uma tecnologia chamada OpenClaw no mercado.

A tecnologia correta que corresponde à descrição usada no documento é:
**Whisper** — modelo de STT open-source da OpenAI.

Características que batem com a justificativa do documento:
- Open-source ✅
- Processamento local (edge) ✅  
- Controle sobre dados sensíveis (LGPD) ✅
- Baixa latência ✅
- Customizável para contexto específico ✅
- Suporte a português ✅

**Ação necessária:** substituir "OpenClaw" por "Whisper (OpenAI)" em toda a Seção 7.

