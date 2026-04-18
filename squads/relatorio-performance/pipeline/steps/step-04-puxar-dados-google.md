---
step: "04"
name: "Puxar Dados Google Ads"
type: agent
agent: analista
condition: "plataforma inclui google"
outputFile: output/dados-google.md
---

# Step 04 — Puxar Dados Google Ads

## Variáveis necessárias (do step-01)

- `CUSTOMER_ID` = custom_fields["ID Cliente Google"]
- `DATA_INICIO` = período início (formato YYYY-MM-DD)
- `DATA_FIM` = período fim (formato YYYY-MM-DD)

## Executar via Bash

```bash
python3 ~/.claude/skills/google-ads/get_campaign_insights.py \
  --customer-id "{CUSTOMER_ID}" \
  --since "{DATA_INICIO}" \
  --until "{DATA_FIM}"
```

## Métricas a extrair por campanha

| Métrica | Descrição |
|---|---|
| Impressões | Exibições totais |
| Cliques | Cliques totais |
| CTR | Taxa de clique |
| CPC médio | Custo médio por clique |
| Investimento | Valor gasto |
| Conversões | Resultados principais |
| CPA | Custo por aquisição/conversão |
| Taxa de conversão | Conversões / cliques |
| Impressões por posição | Para Search |
| Parcela de impressões | Share of voice |

## Se API indisponível

Registrar limitação. Solicitar ao usuário que exporte o relatório manualmente do painel e anexe na task.

```
clickup_create_task_comment(task_id,
  "⚠️ API Google Ads indisponível. Para completar o relatório, exporte os dados do período {DATA_INICIO} a {DATA_FIM} em: Google Ads > Relatórios > Campanhas e anexe o CSV nesta task.")
```

## Salvar em output/dados-google.md
