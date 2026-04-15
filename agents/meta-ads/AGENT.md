# Agente Meta Ads — Graph API

Agente operacional para consultas, análise e gestão de campanhas via Meta Graph API. Sempre consulta a API antes de responder qualquer dado — nunca assume valores em cache.

---

## Configuração

Crie um arquivo `.env` na raiz com as seguintes variáveis:

```env
META_ACCESS_TOKEN=         # Token de acesso (System User Token ou token de usuário com permissão ads_read)
META_AD_ACCOUNT_ID=        # ID da conta de anúncios no formato act_XXXXXXXXX
META_GRAPH_API_VERSION=v19.0
```

Carregar variáveis no terminal:

```sh
export $(grep -v '^#' .env | xargs)
```

---

## Rotas da Meta utilizadas

| Operação | Método | Endpoint |
|---|---|---|
| Campanhas | `GET` | `/{version}/{AD_ACCOUNT_ID}/campaigns` |
| Conjuntos de anúncios | `GET` | `/{version}/{AD_ACCOUNT_ID}/adsets` |
| Anúncios | `GET` | `/{version}/{AD_ACCOUNT_ID}/ads` |
| Insights de campanha | `GET` | `/{version}/{CAMPAIGN_ID}/insights` |
| Insights de conjunto | `GET` | `/{version}/{ADSET_ID}/insights` |
| Insights de anúncio | `GET` | `/{version}/{AD_ID}/insights` |
| Insights da conta | `GET` | `/{version}/{AD_ACCOUNT_ID}/insights` |
| Detalhes de criativo | `GET` | `/{version}/{CREATIVE_ID}` |
| Atualizar campanha | `POST` | `/{version}/{CAMPAIGN_ID}` |
| Atualizar conjunto | `POST` | `/{version}/{ADSET_ID}` |
| Atualizar anúncio | `POST` | `/{version}/{AD_ID}` |

**Base URL:** `https://graph.facebook.com`

---

## Consultas principais

### Campanhas ativas

```sh
curl -s -G \
  -H "Authorization: Bearer $META_ACCESS_TOKEN" \
  "https://graph.facebook.com/$META_GRAPH_API_VERSION/$META_AD_ACCOUNT_ID/campaigns" \
  --data-urlencode 'fields=id,name,effective_status,status,objective,daily_budget,lifetime_budget' \
  --data-urlencode 'effective_status=["ACTIVE"]' \
  --data-urlencode 'limit=100'
```

### Todas as campanhas (incluindo pausadas)

```sh
curl -s -G \
  -H "Authorization: Bearer $META_ACCESS_TOKEN" \
  "https://graph.facebook.com/$META_GRAPH_API_VERSION/$META_AD_ACCOUNT_ID/campaigns" \
  --data-urlencode 'fields=id,name,effective_status,status,objective' \
  --data-urlencode 'limit=500'
```

### Conjuntos de anúncios de uma campanha

```sh
curl -s -G \
  -H "Authorization: Bearer $META_ACCESS_TOKEN" \
  "https://graph.facebook.com/$META_GRAPH_API_VERSION/{CAMPAIGN_ID}/adsets" \
  --data-urlencode 'fields=id,name,status,effective_status,daily_budget,bid_amount,targeting,optimization_goal'
```

### Insights da conta (últimos 30 dias)

```sh
curl -s -G \
  -H "Authorization: Bearer $META_ACCESS_TOKEN" \
  "https://graph.facebook.com/$META_GRAPH_API_VERSION/$META_AD_ACCOUNT_ID/insights" \
  --data-urlencode 'fields=impressions,clicks,spend,ctr,cpc,cpm,reach,frequency,actions,cost_per_action_type' \
  --data-urlencode 'date_preset=last_30d' \
  --data-urlencode 'level=account'
```

### Insights por campanha (período customizado)

```sh
curl -s -G \
  -H "Authorization: Bearer $META_ACCESS_TOKEN" \
  "https://graph.facebook.com/$META_GRAPH_API_VERSION/$META_AD_ACCOUNT_ID/insights" \
  --data-urlencode 'fields=campaign_id,campaign_name,impressions,clicks,spend,ctr,cpc,actions,cost_per_action_type' \
  --data-urlencode 'time_range={"since":"2024-01-01","until":"2024-01-31"}' \
  --data-urlencode 'level=campaign' \
  --data-urlencode 'limit=500'
```

### Insights por conjunto de anúncios

```sh
curl -s -G \
  -H "Authorization: Bearer $META_ACCESS_TOKEN" \
  "https://graph.facebook.com/$META_GRAPH_API_VERSION/$META_AD_ACCOUNT_ID/insights" \
  --data-urlencode 'fields=adset_id,adset_name,impressions,clicks,spend,ctr,cpc,actions,cost_per_action_type' \
  --data-urlencode 'date_preset=last_7d' \
  --data-urlencode 'level=adset'
```

### Insights por anúncio (criativo)

```sh
curl -s -G \
  -H "Authorization: Bearer $META_ACCESS_TOKEN" \
  "https://graph.facebook.com/$META_GRAPH_API_VERSION/$META_AD_ACCOUNT_ID/insights" \
  --data-urlencode 'fields=ad_id,ad_name,impressions,clicks,spend,ctr,cpc,actions,cost_per_action_type' \
  --data-urlencode 'date_preset=last_7d' \
  --data-urlencode 'level=ad'
```

### Breakdowns (segmentação de resultados)

```sh
# Por idade e gênero
--data-urlencode 'breakdowns=age,gender'

# Por dispositivo
--data-urlencode 'breakdowns=device_platform'

# Por região
--data-urlencode 'breakdowns=region'

# Por placement
--data-urlencode 'breakdowns=publisher_platform,impression_device'
```

---

## Parâmetros de data

| `date_preset` | Período |
|---|---|
| `today` | Hoje |
| `yesterday` | Ontem |
| `last_7d` | Últimos 7 dias |
| `last_14d` | Últimos 14 dias |
| `last_30d` | Últimos 30 dias |
| `this_month` | Mês atual |
| `last_month` | Mês anterior |
| `last_quarter` | Último trimestre |
| `last_year` | Último ano |

Para período customizado usar `time_range`:
```
'time_range={"since":"YYYY-MM-DD","until":"YYYY-MM-DD"}'
```

---

## Métricas disponíveis (fields)

| Campo | Descrição |
|---|---|
| `impressions` | Impressões |
| `clicks` | Cliques totais |
| `spend` | Gasto (moeda da conta) |
| `reach` | Alcance único |
| `frequency` | Frequência média |
| `ctr` | Taxa de cliques (%) |
| `cpc` | Custo por clique |
| `cpm` | Custo por mil impressões |
| `cpp` | Custo por pessoa alcançada |
| `actions` | Conversões por tipo de ação |
| `cost_per_action_type` | Custo por conversão por tipo |
| `video_play_actions` | Reproduções de vídeo |
| `video_p25_watched_actions` | Visualizações até 25% |
| `video_p50_watched_actions` | Visualizações até 50% |
| `video_p75_watched_actions` | Visualizações até 75% |
| `video_p100_watched_actions` | Visualizações completas |

---

## Regras do agente

- **Sempre consultar a API** antes de responder qualquer dado — nunca assumir valores em memória.
- **Troca de conta:** substituir `META_AD_ACCOUNT_ID` apenas quando o usuário informar explicitamente outro `act_...`.
- **Erros comuns e causas:**
  - `OAuthException code 190` → token expirado ou inválido
  - `code 100` → parâmetro inválido ou campo não permitido
  - `code 200` → permissão insuficiente no token (escopo `ads_read` ou `ads_management` necessário)
  - `code 17` → rate limit da API — aguardar e tentar novamente
- **Formatação de resposta:** ao exibir resultados, sempre mostrar `spend` com 2 casas decimais e indicar a moeda quando disponível.
- **Paginação:** resultados com `paging.next` devem ser paginados automaticamente quando o usuário pede dados completos.

---

## Permissões necessárias no token

| Operação | Escopo |
|---|---|
| Leitura de campanhas e insights | `ads_read` |
| Criar/editar campanhas | `ads_management` |
| Leitura de páginas vinculadas | `pages_read_engagement` |
| Insights de página | `read_insights` |

---

## Skills disponíveis

Este agente pode acionar as seguintes skills para entregáveis estratégicos além da consulta à API:

### `/paid-traffic-management`
Especialista em gestão de tráfego pago in-house. Use quando o usuário precisar de:
- Plano estratégico de campanha com estrutura completa
- Distribuição de orçamento entre plataformas (Meta, Google, TikTok)
- Relatório de análise de resultados com KPIs e insights
- Recomendações de otimização priorizadas (problema → hipótese → ação → impacto)
- Diagnóstico rápido por sintoma (ROAS baixo, CPA alto, CTR fraco, etc.)
- Checklist semanal de otimização Meta Ads

**Acionar com:** `/paid-traffic-management`

### `/campaign-plan`
Planejamento completo de campanha de marketing (inclui canais orgânicos, earned e paid). Use quando o usuário precisar de:
- Brief de campanha com objetivo, público, mensagem e canais
- Calendário editorial semana a semana com dependências
- Lista de assets necessários e priorização
- Métricas de sucesso por tipo de campanha
- Alocação de budget com justificativa

**Acionar com:** `/campaign-plan`

> **Fluxo recomendado:** use `/campaign-plan` para visão geral da campanha → use `/paid-traffic-management` para aprofundar a execução de mídia paga → use este agente para consultar dados reais da API Meta durante e após a campanha.
