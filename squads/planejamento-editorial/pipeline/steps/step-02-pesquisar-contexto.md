---
step: "02"
name: "Pesquisar Contexto e Tendências"
type: agent
agent: ogilvy
execution: inline
depends_on: step-01
outputFile: output/contexto.md
---

# Step 02 — Ogilvy: Pesquisar Contexto e Tendências

## Para o Pipeline Runner

Ogilvy pesquisa o contexto do mês para o segmento do cliente antes de criar a pauta.
O objetivo é garantir relevância cultural e identificar oportunidades sazonais.

## O que pesquisar

### 1. Datas e efemérides do mês
- Feriados nacionais e datas comemorativas relevantes para o segmento
- Eventos do mercado (lançamentos, premiações, tendências do setor)
- Datas de marketing estabelecidas (Dia das Mães, Black Friday, etc.)

### 2. Tendências do segmento
- Formatos de conteúdo em alta no Instagram para o nicho do cliente
- Temas em debate na comunidade do segmento
- Hashtags com bom volume e engajamento no setor

### 3. Performance histórica (se disponível em memória)
- Quais pilares geraram mais engajamento nos meses anteriores
- Formatos que o público do cliente mais responde
- Horários e dias com melhor alcance

## Skills a usar

- `33-marketing-concorrentes` — se o cliente tiver concorrentes mapeados na memória
- `web_search` — para tendências atuais do segmento (usar com data do mês de referência)

## Regras

- Não inventar tendências — só registrar o que for verificável
- Se não houver dados históricos suficientes, indicar "sem dados" e prosseguir
- Limitar pesquisa a 10–15 minutos equivalentes de busca

## Output esperado

Salvar em `output/contexto.md`:

```markdown
# Contexto Editorial — [Cliente] — [Mês/Ano]

## Datas e Efemérides
- [data]: [evento] — oportunidade: [sim/não] — por quê: [razão]

## Tendências do Segmento
- [tendência]: [relevância para o cliente]

## Insights de Performance (histórico)
- [insight baseado em _memory/memories.md]

## Oportunidades Identificadas
- [oportunidade] → sugestão de tema/formato
```
