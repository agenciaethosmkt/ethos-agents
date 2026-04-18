---
step: "03"
name: "Processar Dados de Campanha"
type: agent
agent: analista
outputFile: output/dados-campanha.md
---

# Step 03 — Processar Dados de Campanha

## Fonte 1 — Planilha de dados no Drive

Padrão: `[CLIENTE] - Dados Campanha`

Estrutura conhecida (Google Ads):
- Day, Campaign Name, Ad Group Name, Ad Name, Advertising Channel
- Clicks, Impressions, CTR, Avg. CPC, Cost (Spend)
- Conversions, View-through conv., Cost/conv., Conv. rate

```
mcp__claude_ai_Google_Drive__search_files(
  query="title contains '{cliente_nome}' and title contains 'Dados Campanha'"
)
→ mcp__claude_ai_Google_Drive__read_file_content(file_id)
```

### Calcular totais da planilha

```python
# Agregar por período completo:
total_impressoes    = somar coluna Impressions
total_cliques       = somar coluna Clicks
ctr_medio           = total_cliques / total_impressoes * 100
cpc_medio           = média ponderada de Avg. CPC (por cliques)
investimento_total  = somar coluna Cost
total_conversoes    = somar coluna Conversions
cpl                 = investimento_total / total_conversoes  # se conversoes > 0
taxa_conv_campanha  = total_conversoes / total_cliques * 100

# Por plataforma (se misto):
google_spend        = somar Cost onde Channel == "Search" ou "Display"
meta_spend          = somar Cost onde Channel == "Social" ou registro separado
```

---

## Fonte 2 — API Meta Ads (se credenciais disponíveis)

Se `custom_fields["Token Meta"]` e `custom_fields["ID BM Meta"]` presentes:

```bash
python3 ~/.claude/skills/meta-ads/get_campaign_insights.py \
  --bm-id "{ID_BM}" \
  --token "{TOKEN}" \
  --since "{data_inicio}" \
  --until "{data_fim}" \
  --fields "impressions,reach,clicks,spend,actions,cost_per_action_type,ctr,cpc,cpm,frequency"
```

---

## Fonte 3 — API Google Ads (se credenciais disponíveis)

```bash
python3 ~/.claude/skills/google-ads/get_campaign_insights.py \
  --customer-id "{CUSTOMER_ID}" \
  --since "{data_inicio}" \
  --until "{data_fim}"
```

---

## Output — salvar em output/dados-campanha.md

```markdown
# Dados de Campanha — [Cliente] — [Período]

## Resumo geral
- Investimento total: R$ [valor]
- Impressões: [X]
- Cliques: [X]
- CTR médio: [%]
- CPC médio: R$ [valor]
- Conversões rastreadas: [X]
- CPL (custo por lead): R$ [valor]

## Por plataforma
| Plataforma | Investimento | Leads | CPL |
|---|---|---|---|
| Google Ads | R$ [X] | [X] | R$ [X] |
| Meta Ads | R$ [X] | [X] | R$ [X] |

## Período dos dados
[data_inicio] → [data_fim]

## Fontes utilizadas
- [ ] Planilha Drive: [nome]
- [ ] API Meta Ads
- [ ] API Google Ads
```

## Se nenhuma fonte disponível

```
clickup_create_task_comment(task_id,
  "⚠️ Nenhuma planilha de campanha encontrada e sem credenciais de API. Case será gerado apenas com dados de leads.")
```
