---
step: "05"
name: "Redigir Case"
type: agent
agent: redator
inputFiles:
  - output/metricas.md
  - output/dados-leads.md
  - output/dados-campanha.md
outputFile: output/case.md
---

# Step 05 — Redigir Case para Prova Social

## Objetivo

Transformar os dados em narrativa que sirva para:
1. **Prova social em propostas** — lead do mesmo segmento lê e se identifica
2. **Portfólio da Ethos** — documento que pode ser compartilhado publicamente

## Verificar se existe pesquisa NPS do cliente

```
mcp__claude_ai_Google_Drive__search_files(
  query="title contains '{cliente_nome}' and title contains 'NPS'"
)
```

Se encontrar → extrair:
- `nota_nps` — nota de satisfação (0–10)
- `faturamento_entrada` — faturamento quando entrou na Ethos
- `faturamento_atual` — faturamento no momento da pesquisa
- `depoimento` — frase livre do cliente
- `crescimento_faturamento` = ((fat_atual - fat_entrada) / fat_entrada) * 100

> ⚠️ **Dado mais poderoso de um case:** crescimento de faturamento antes/depois.
> Quando disponível via NPS, usar como destaque principal.
> Enquanto o NPS não estiver implementado, o case usa dados de campanha e leads.

---

## Estrutura do case

```markdown
# Case Ethos — [Segmento] — [Período]
<!-- Nome do cliente: usar se autorizado. Padrão: "Eletricista em São Paulo" -->

## Situação antes da Ethos

[2–3 linhas: como chegavam clientes, o que não funcionava, por que buscaram a Ethos]

Exemplo:
> Um eletricista autônomo em São Paulo dependia exclusivamente de indicação.
> Nos meses fracos, a agenda ficava vazia e a receita imprevisível.
> Era invisível para quem procurava eletricista no Google.

## O que a Ethos fez

[2–3 linhas: plataformas, tipo de campanha, foco — sem jargão]

Exemplo:
> Criamos campanhas no Google Ads focadas em buscas locais de emergência e serviços específicos.
> Estruturamos o processo de atendimento para converter leads em orçamentos e vendas.

## Resultados em [X semanas/meses]

| Métrica | Resultado |
|---|---|
| Leads gerados | [X] |
| Negócios fechados | [X] ([X]% de conversão) |
| Receita gerada | R$ [X] |
| CPL | R$ [X] |
| Investimento total | R$ [X] |
| ROI | [X]% |
<!-- Se NPS disponível: -->
| Crescimento de faturamento | +[X]% |

**Destaque:** [1 frase com o número mais impactante]

<!-- Se depoimento disponível via NPS: -->
## Em palavras do cliente
> "[depoimento direto]"

## Dados técnicos
- Segmento: [segmento]
- Plano: [Flow / Growth]
- Período: [início] → [fim] ([X] meses)
- Fontes: [planilha leads / dados campanha / NPS]
```

---

## Regras

- **Nunca inventar** — usar apenas dados de output/metricas.md
- **Anonimizar por padrão** — segmento + cidade, não nome (aguardar autorização de Renato no checkpoint)
- **Período curto** (< 4 semanas) → indicar "resultados iniciais" no case
- **Sem NPS ainda** → omitir seção de faturamento, não inventar
