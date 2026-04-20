# ADR-001 — Arquitetura Offline-First no Edge

| Campo | Valor |
|-------|-------|
| **Status** | ✅ Aceita |
| **Data** | 2026-03-01 |
| **Autores** | Leonardo Turbiani (RM366050) |
| **Revisores** | Grupo 18 — 2TCMT |
| **Contexto** | Fase 5 — SmartGate · Tech Challenge 2TCMT |

---

## Contexto

O SmartGate opera em 20 condomínios distribuídos em São Paulo. Cada condomínio depende de conectividade de internet, mas falhas de rede são eventos esperados em operações de segurança física. Uma arquitetura **cloud-first** — onde cada decisão de acesso requer chamada à nuvem — cria uma dependência crítica:

> Se a internet cair, o acesso fica **bloqueado** (falha fechada) ou **irrestrito** (falha aberta).

Ambos os cenários são inaceitáveis em um sistema de segurança de alto padrão.

Além disso, latência de chamada de rede (100–800ms) é incompatível com a meta de autorização em < 500ms exigida pela experiência do usuário.

---

## Decisão

Adotamos **Edge-First com sincronização assíncrona** para a nuvem:

### O que roda localmente (Edge Node — NVIDIA Jetson Orin):
- Reconhecimento facial offline (modelo YOLO + embeddings locais)
- Orquestração do fluxo de acesso (Edge Orchestrator)
- Persistência de eventos (SQLite em WAL mode — durável em crash)
- Whitelist de visitantes autorizados (atualizada a cada 15 min quando online)
- Regras de acesso determinísticas
- Controle direto dos dispositivos físicos (MQTT local)

### O que a nuvem potencializa (quando conectado):
- Reconhecimento facial de segunda camada (AWS Rekognition)
- Push notifications em tempo real (Firebase)
- Sincronização de eventos para auditoria central
- Atualizações de regras e configurações
- Análise de anomalias cross-condomínio

---

## Alternativas Consideradas

| Alternativa | Motivo de Rejeição |
|-------------|-------------------|
| **Cloud-first** (toda decisão na nuvem) | Inviável: falha de rede = falha de segurança. Latência incompatível com UX |
| **Thin client** (apenas câmera no edge) | Latência > 2s para interação do visitante; dependência total da nuvem |
| **Sem edge** (operador decide tudo) | Mantém o problema central do TC: dependência humana irrestrita |
| **Edge autônomo sem sync** | Impossibilita auditoria centralizada e análise cross-condomínio |

---

## Consequências

### Positivas ✅
- Operação garantida com 100% de perda de conectividade
- Latência de decisão < 500ms (processamento local com GPU)
- Redução de custo de banda (envia eventos, não stream de vídeo)
- Maior controle de dados sensíveis (LGPD — biometria não sai do perímetro)

### Negativas / Trade-offs ⚠️
- Hardware adicional por condomínio (~R$ 8.000 por Jetson Orin)
- Complexidade de sincronização e reconciliação de estados
- Necessidade de atualização de firmware nos edge nodes
- Whitelist pode ter gap de até 15 min entre atualizações

### Modo Degradado
Quando a conectividade é perdida, o sistema opera em três estados:
1. **Online** → operação normal
2. **Degradado** (timeout < 30s) → usa cache local, notifica por SMS fallback
3. **Offline** → decisão 100% local, acessos "condicionais" revisados no resync

---

## Critério de Revisão

Reavaliar se:
- Custo do hardware edge se tornar proibitivo em escala > 100 condomínios
- Provedores oferecerem SLA de 99,99% com link redundante
- Modelos de IA em nuvem atingirem latência < 50ms (5G edge)
