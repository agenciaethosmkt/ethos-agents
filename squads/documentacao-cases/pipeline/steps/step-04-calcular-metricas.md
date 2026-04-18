---
step: "04"
name: "Calcular Métricas Consolidadas"
type: agent
agent: analista
inputFiles:
  - output/dados-leads.md
  - output/dados-campanha.md
outputFile: output/metricas.md
---

# Step 04 — Calcular Métricas Consolidadas do Período

## Cruzar planilha de leads com dados de campanha

```python
# Métricas consolidadas:
total_leads_gerados  = total_leads (planilha) OU conversoes_rastreadas (campanha)
                       → usar o maior valor entre os dois (planilha é mais confiável)
taxa_conversao       = leads_fechados / total_leads_gerados * 100
receita_total        = soma dos valores de venda (planilha RESUMO)
ticket_medio         = receita_total / leads_fechados
investimento_total   = soma do custo de campanha
roi                  = (receita_total - investimento_total) / investimento_total * 100
cpl_real             = investimento_total / total_leads_gerados
cpa_real             = investimento_total / leads_fechados  # custo por venda fechada
```

## Comparar com benchmarks do segmento

Usar `pipeline/data/benchmarks-por-segmento.md`:

```
cpl_benchmark = benchmark do segmento
cpl_cliente   = cpl_real calculado
variacao_cpl  = (cpl_benchmark - cpl_cliente) / cpl_benchmark * 100
```

## Construir narrativa de resultado

Transformar números em frases:

| Métrica | Dado | Narrativa |
|---|---|---|
| CPL | R$12 (benchmark R$25) | "CPL 52% abaixo da média do setor" |
| Taxa conversão | 35% | "1 em cada 3 leads virou cliente" |
| Receita | R$2.010 em X semanas | "R$2.010 em receita gerada" |
| ROI | 340% | "R$3,40 de retorno para cada R$1 investido" |

## Output — salvar em output/metricas.md

```markdown
# Métricas Consolidadas — [Cliente] — [Período]

## Números do período ([X] meses / semanas)

| Métrica | Resultado | vs Benchmark |
|---|---|---|
| Leads gerados | [X] | — |
| Taxa de conversão | [X]% | [benchmark]% |
| Negócios fechados | [X] | — |
| Receita gerada | R$ [X] | — |
| Ticket médio | R$ [X] | — |
| Investimento | R$ [X] | — |
| CPL | R$ [X] | R$ [benchmark] ([±X]%) |
| CPA (custo por venda) | R$ [X] | — |
| ROI | [X]% | — |

## Narrativa de destaque
[2–3 frases que resumem o resultado em linguagem do cliente]

## Dados por plataforma
| Plataforma | Leads | Conversões | CPL |
|---|---|---|---|
| Google Ads | [X] | [X] | R$ [X] |
| Meta Ads | [X] | [X] | R$ [X] |

## Limitações dos dados
[campos ausentes, estimativas usadas, período parcial, etc.]
```
