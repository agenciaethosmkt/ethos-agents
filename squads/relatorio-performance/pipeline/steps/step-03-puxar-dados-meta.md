---
step: "03"
name: "Puxar Dados Meta Ads"
type: agent
agent: analista
condition: "plataforma inclui meta"
outputFile: output/dados-meta.md
---

# Step 03 — Puxar Dados Meta Ads

## Variáveis necessárias (do step-01)

- `BM_ID` = custom_fields["ID BM Meta"]
- `TOKEN` = custom_fields["Token Meta"]
- `DATA_INICIO` = período início (formato YYYY-MM-DD)
- `DATA_FIM` = período fim (formato YYYY-MM-DD)

## Executar via Bash

```bash
python3 ~/.claude/skills/meta-ads/get_campaign_insights.py \
  --bm-id "{BM_ID}" \
  --token "{TOKEN}" \
  --since "{DATA_INICIO}" \
  --until "{DATA_FIM}" \
  --fields "campaign_name,impressions,reach,clicks,spend,ctr,cpc,cpm,frequency,actions,cost_per_action_type,video_play_actions,video_avg_time_watched_actions" \
  --level campaign
```

## Métricas a extrair por campanha

| Métrica | Campo API | Descrição |
|---|---|---|
| Impressões | impressions | Quantas vezes foi exibido |
| Alcance | reach | Pessoas únicas atingidas |
| Cliques | clicks | Cliques totais no anúncio |
| CTR | ctr | Taxa de clique |
| CPC | cpc | Custo por clique |
| CPM | cpm | Custo por mil impressões |
| Frequência | frequency | Média de vezes visto por pessoa |
| Investimento | spend | Valor gasto no período |
| Conversões | actions[purchase/lead/etc] | Resultado principal |
| CPA/CPL | cost_per_action_type | Custo por resultado |
| Retenção de vídeo | video_avg_time_watched | Para Reels/Stories |

## Se a API retornar erro

Registrar o erro e continuar com dados parciais. Nunca inventar métricas.

```
# Dados Meta Ads — [Cliente] — {DATA_INICIO} a {DATA_FIM}
[dados retornados pela API]

## Erros encontrados
[descrever erros, se houver]
```

## Salvar em output/dados-meta.md
