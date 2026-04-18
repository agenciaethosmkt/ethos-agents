---
step: "05"
name: "Interpretar Métricas"
type: agent
agent: analista
inputFiles:
  - output/dados-meta.md
  - output/dados-google.md
outputFile: output/analise.md
---

# Step 05 — Interpretar Métricas

## Objetivo

Transformar dados brutos em insights acionáveis. Não apenas "o que aconteceu" — mas "o que isso significa" e "o que fazer".

## Análise por plataforma

### Meta Ads

#### Benchmarks de referência (ajustar por setor do cliente)

| Métrica | Abaixo da média | Médio | Acima da média |
|---|---|---|---|
| CTR (Feed) | < 0.8% | 0.8–2% | > 2% |
| CTR (Stories) | < 0.3% | 0.3–0.8% | > 0.8% |
| Frequência | > 4 | 2–4 | < 2 |
| CPM | > R$40 | R$15–40 | < R$15 |
| Taxa de retenção vídeo (3s) | < 20% | 20–40% | > 40% |

#### Sinalizadores a identificar

- **Fadiga de criativo**: frequência > 3.5 + CTR caindo → recomendar novos criativos
- **Público saturado**: alcance crescendo lentamente + CPM subindo → revisar segmentação
- **Criativo com potencial**: CTR alto + CPM baixo → aumentar budget
- **Problema de destino**: CTR bom + conversões baixas → verificar landing page

### Google Ads

#### Sinalizadores a identificar

- **Parcela de impressões baixa**: budget limitado, aumentar ou reduzir lances
- **CTR abaixo do setor**: revisar headlines e extensões
- **CPA acima da meta**: revisar palavras-chave negativas, lances, landing page
- **Taxa de conversão caindo**: possível problema na página de destino

## Estrutura da análise

```markdown
# Análise de Performance — [Cliente] — [Período]

## Resumo executivo
[3–5 linhas: o que aconteceu no período, resultado principal, contexto]

## Destaques positivos
- [insight 1 com dado]
- [insight 2 com dado]

## Pontos de atenção
- [problema 1 com dado + causa provável]
- [problema 2 com dado + causa provável]

## Recomendações
1. [ação específica] — impacto esperado: [resultado]
2. [ação específica] — impacto esperado: [resultado]

## Dados completos por campanha
[tabela com todas as métricas]
```

## Regra de ouro

Nunca apresentar dado sem contexto. Sempre responder: "isso é bom ou ruim? Por quê? O que fazer?"
