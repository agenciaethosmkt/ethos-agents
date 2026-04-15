# Agente Google Ads — Google Ads API

Agente operacional para consultas, análise e gestão de campanhas via Google Ads API. Sempre consulta a API antes de responder qualquer dado — nunca assume valores em cache.

---

## Configuração

Crie um arquivo `.env` na raiz com as seguintes variáveis:

```env
GOOGLE_ADS_DEVELOPER_TOKEN=    # Token de desenvolvedor — Google Ads > Ferramentas > Central da API
GOOGLE_ADS_CUSTOMER_ID=        # ID da conta de anúncios sem traços (ex: 1234567890)
GOOGLE_ADS_LOGIN_CUSTOMER_ID=  # ID da conta MCC/gerenciadora (se aplicável, sem traços)
GOOGLE_ADS_CLIENT_ID=          # OAuth2 Client ID — Google Cloud Console
GOOGLE_ADS_CLIENT_SECRET=      # OAuth2 Client Secret — Google Cloud Console
GOOGLE_ADS_REFRESH_TOKEN=      # OAuth2 Refresh Token gerado via OAuth2 Playground
GOOGLE_ADS_API_VERSION=v23
```

Carregar variáveis no terminal:

```sh
export $(grep -v '^#' .env | xargs)
```

Obter access token a partir do refresh token:

```sh
ACCESS_TOKEN=$(curl -s -X POST "https://oauth2.googleapis.com/token" \
  -d "client_id=$GOOGLE_ADS_CLIENT_ID" \
  -d "client_secret=$GOOGLE_ADS_CLIENT_SECRET" \
  -d "refresh_token=$GOOGLE_ADS_REFRESH_TOKEN" \
  -d "grant_type=refresh_token" | jq -r '.access_token')
```

> **Sempre obtenha um `ACCESS_TOKEN` fresco antes de cada bloco de chamadas** — o token expira em 1 hora.

---

## Autenticação — Headers obrigatórios

```
Authorization: Bearer {ACCESS_TOKEN}
developer-token: {GOOGLE_ADS_DEVELOPER_TOKEN}
login-customer-id: {GOOGLE_ADS_LOGIN_CUSTOMER_ID}   # apenas se usar MCC
Content-Type: application/json
```

---

## Base URL

```
https://googleads.googleapis.com/{GOOGLE_ADS_API_VERSION}/customers/{GOOGLE_ADS_CUSTOMER_ID}
```

---

## Linguagem de consulta — GAQL

A Google Ads API usa **GAQL (Google Ads Query Language)**, similar ao SQL.

```sql
SELECT resource.field, metrics.metric
FROM resource_name
WHERE segments.date DURING LAST_30_DAYS
  AND campaign.status = 'ENABLED'
ORDER BY metrics.cost_micros DESC
LIMIT 100
```

Todas as consultas são feitas via:

```sh
POST /customers/{CUSTOMER_ID}/googleAds:search
Body: { "query": "SELECT ..." }
```

> **Atenção:** valores monetários são retornados em **micros** (1 BRL = 1.000.000 micros). Sempre dividir por 1.000.000 ao exibir.

---

## Consultas principais

### Campanhas ativas

```sh
curl -s -X POST \
  "https://googleads.googleapis.com/$GOOGLE_ADS_API_VERSION/customers/$GOOGLE_ADS_CUSTOMER_ID/googleAds:search" \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "developer-token: $GOOGLE_ADS_DEVELOPER_TOKEN" \
  -H "login-customer-id: $GOOGLE_ADS_LOGIN_CUSTOMER_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "SELECT campaign.id, campaign.name, campaign.status, campaign.advertising_channel_type, campaign_budget.amount_micros FROM campaign WHERE campaign.status = '\''ENABLED'\'' ORDER BY campaign.name LIMIT 100"
  }'
```

### Todas as campanhas (incluindo pausadas)

```sh
curl -s -X POST \
  "https://googleads.googleapis.com/$GOOGLE_ADS_API_VERSION/customers/$GOOGLE_ADS_CUSTOMER_ID/googleAds:search" \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "developer-token: $GOOGLE_ADS_DEVELOPER_TOKEN" \
  -H "login-customer-id: $GOOGLE_ADS_LOGIN_CUSTOMER_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "SELECT campaign.id, campaign.name, campaign.status, campaign.advertising_channel_type FROM campaign ORDER BY campaign.name LIMIT 500"
  }'
```

### Performance da conta (últimos 30 dias)

```sh
curl -s -X POST \
  "https://googleads.googleapis.com/$GOOGLE_ADS_API_VERSION/customers/$GOOGLE_ADS_CUSTOMER_ID/googleAds:search" \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "developer-token: $GOOGLE_ADS_DEVELOPER_TOKEN" \
  -H "login-customer-id: $GOOGLE_ADS_LOGIN_CUSTOMER_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "SELECT metrics.impressions, metrics.clicks, metrics.cost_micros, metrics.ctr, metrics.average_cpc, metrics.conversions, metrics.cost_per_conversion FROM customer WHERE segments.date DURING LAST_30_DAYS"
  }'
```

### Performance por campanha (período customizado)

```sh
curl -s -X POST \
  "https://googleads.googleapis.com/$GOOGLE_ADS_API_VERSION/customers/$GOOGLE_ADS_CUSTOMER_ID/googleAds:search" \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "developer-token: $GOOGLE_ADS_DEVELOPER_TOKEN" \
  -H "login-customer-id: $GOOGLE_ADS_LOGIN_CUSTOMER_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "SELECT campaign.id, campaign.name, metrics.impressions, metrics.clicks, metrics.cost_micros, metrics.ctr, metrics.average_cpc, metrics.conversions, metrics.cost_per_conversion FROM campaign WHERE segments.date BETWEEN '\''2024-01-01'\'' AND '\''2024-01-31'\'' ORDER BY metrics.cost_micros DESC LIMIT 500"
  }'
```

### Performance por grupo de anúncios

```sh
curl -s -X POST \
  "https://googleads.googleapis.com/$GOOGLE_ADS_API_VERSION/customers/$GOOGLE_ADS_CUSTOMER_ID/googleAds:search" \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "developer-token: $GOOGLE_ADS_DEVELOPER_TOKEN" \
  -H "login-customer-id: $GOOGLE_ADS_LOGIN_CUSTOMER_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "SELECT campaign.name, ad_group.id, ad_group.name, ad_group.status, metrics.impressions, metrics.clicks, metrics.cost_micros, metrics.ctr, metrics.average_cpc, metrics.conversions FROM ad_group WHERE segments.date DURING LAST_7_DAYS ORDER BY metrics.cost_micros DESC LIMIT 200"
  }'
```

### Performance por anúncio (criativo)

```sh
curl -s -X POST \
  "https://googleads.googleapis.com/$GOOGLE_ADS_API_VERSION/customers/$GOOGLE_ADS_CUSTOMER_ID/googleAds:search" \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "developer-token: $GOOGLE_ADS_DEVELOPER_TOKEN" \
  -H "login-customer-id: $GOOGLE_ADS_LOGIN_CUSTOMER_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "SELECT campaign.name, ad_group.name, ad_group_ad.ad.id, ad_group_ad.ad.type, metrics.impressions, metrics.clicks, metrics.cost_micros, metrics.ctr, metrics.conversions FROM ad_group_ad WHERE segments.date DURING LAST_7_DAYS ORDER BY metrics.cost_micros DESC LIMIT 200"
  }'
```

### Performance por palavra-chave

```sh
curl -s -X POST \
  "https://googleads.googleapis.com/$GOOGLE_ADS_API_VERSION/customers/$GOOGLE_ADS_CUSTOMER_ID/googleAds:search" \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "developer-token: $GOOGLE_ADS_DEVELOPER_TOKEN" \
  -H "login-customer-id: $GOOGLE_ADS_LOGIN_CUSTOMER_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "SELECT campaign.name, ad_group.name, ad_group_criterion.keyword.text, ad_group_criterion.keyword.match_type, metrics.impressions, metrics.clicks, metrics.cost_micros, metrics.ctr, metrics.average_cpc, metrics.conversions FROM keyword_view WHERE segments.date DURING LAST_30_DAYS ORDER BY metrics.cost_micros DESC LIMIT 500"
  }'
```

### Segmentação por dispositivo

```sh
-d '{
  "query": "SELECT campaign.name, segments.device, metrics.impressions, metrics.clicks, metrics.cost_micros, metrics.ctr, metrics.conversions FROM campaign WHERE segments.date DURING LAST_30_DAYS"
}'
```

### Segmentação por rede (Search, Display, YouTube)

```sh
-d '{
  "query": "SELECT campaign.name, segments.ad_network_type, metrics.impressions, metrics.clicks, metrics.cost_micros, metrics.ctr FROM campaign WHERE segments.date DURING LAST_30_DAYS"
}'
```

---

## Rotas da Google Ads API utilizadas

| Operação | Método | Endpoint |
|---|---|---|
| Consultar dados (GAQL) | `POST` | `/customers/{id}/googleAds:search` |
| Stream de dados (GAQL) | `POST` | `/customers/{id}/googleAds:searchStream` |
| Mutações (criar/editar) | `POST` | `/customers/{id}/campaigns:mutate` |
| Mutações de grupos | `POST` | `/customers/{id}/adGroups:mutate` |
| Mutações de anúncios | `POST` | `/customers/{id}/adGroupAds:mutate` |
| Orçamentos | `POST` | `/customers/{id}/campaignBudgets:mutate` |
| Recomendações | `GET` | `/customers/{id}/recommendations` |

---

## Parâmetros de data (GAQL)

| `DURING` | Período |
|---|---|
| `TODAY` | Hoje |
| `YESTERDAY` | Ontem |
| `LAST_7_DAYS` | Últimos 7 dias |
| `LAST_14_DAYS` | Últimos 14 dias |
| `LAST_30_DAYS` | Últimos 30 dias |
| `THIS_MONTH` | Mês atual |
| `LAST_MONTH` | Mês anterior |
| `LAST_QUARTER` | Último trimestre |
| `LAST_YEAR` | Último ano |

Para período customizado:
```sql
WHERE segments.date BETWEEN '2024-01-01' AND '2024-01-31'
```

---

## Métricas disponíveis

| Campo | Descrição |
|---|---|
| `metrics.impressions` | Impressões |
| `metrics.clicks` | Cliques |
| `metrics.cost_micros` | Custo em micros (÷ 1.000.000 = valor real) |
| `metrics.ctr` | Taxa de cliques (decimal, ex: 0.05 = 5%) |
| `metrics.average_cpc` | CPC médio em micros |
| `metrics.average_cpm` | CPM médio em micros |
| `metrics.conversions` | Conversões |
| `metrics.cost_per_conversion` | Custo por conversão em micros |
| `metrics.conversion_rate` | Taxa de conversão |
| `metrics.view_through_conversions` | Conversões de visualização |
| `metrics.video_views` | Visualizações de vídeo |
| `metrics.video_view_rate` | Taxa de visualização de vídeo |
| `metrics.interactions` | Interações totais |
| `metrics.interaction_rate` | Taxa de interação |
| `metrics.all_conversions` | Todas as conversões (incluindo indiretas) |
| `metrics.search_impression_share` | Parcela de impressões na pesquisa |
| `metrics.search_rank_lost_impression_share` | Parcela perdida por posição |
| `metrics.search_budget_lost_impression_share` | Parcela perdida por orçamento |
| `metrics.quality_score` | Índice de qualidade (keyword_view) |

---

## Tipos de campanha (advertising_channel_type)

| Valor | Rede |
|---|---|
| `SEARCH` | Rede de Pesquisa |
| `DISPLAY` | Rede de Display |
| `SHOPPING` | Shopping |
| `VIDEO` | YouTube / Vídeo |
| `MULTI_CHANNEL` | Performance Max (PMax) |
| `SMART` | Campanhas inteligentes |
| `DEMAND_GEN` | Demand Gen |

---

## Regras do agente

- **Sempre consultar a API** antes de responder qualquer dado — nunca assumir valores em memória.
- **Sempre obter um `ACCESS_TOKEN` fresco** via refresh token antes de cada sessão de chamadas.
- **Valores monetários em micros:** sempre dividir por 1.000.000 ao exibir (ex: 5.000.000 micros = R$ 5,00).
- **CTR em decimal:** multiplicar por 100 ao exibir (ex: 0.0523 = 5,23%).
- **Troca de conta:** substituir `GOOGLE_ADS_CUSTOMER_ID` apenas quando o usuário informar outro ID explicitamente.
- **Erros comuns e causas:**
  - `UNAUTHENTICATED` → access token expirado — gerar novo via refresh token
  - `PERMISSION_DENIED` → developer token sem acesso à conta ou permissão insuficiente
  - `INVALID_ARGUMENT` → campo GAQL inválido ou incompatível com o resource
  - `QUOTA_EXHAUSTED` → rate limit — aguardar e tentar novamente
  - `RESOURCE_NOT_FOUND` → customer ID incorreto ou sem acesso
- **Formatação de resposta:** exibir `cost_micros` com 2 casas decimais dividido por 1.000.000 e indicar moeda (BRL por padrão).
- **Paginação:** usar `pageToken` da resposta para paginar resultados grandes automaticamente quando o usuário pede dados completos.

---

## Permissões necessárias no OAuth2

| Operação | Scope |
|---|---|
| Leitura de campanhas e relatórios | `https://www.googleapis.com/auth/adwords` |

> A Google Ads API usa um único scope para todas as operações. O nível de acesso (leitura/escrita) é controlado pela permissão do usuário na conta.

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
- Checklist semanal de otimização Google Ads (search terms, Quality Score, auction insights)

**Acionar com:** `/paid-traffic-management`

### `/campaign-plan`
Planejamento completo de campanha de marketing (inclui canais orgânicos, earned e paid). Use quando o usuário precisar de:
- Brief de campanha com objetivo, público, mensagem e canais
- Calendário editorial semana a semana com dependências
- Lista de assets necessários e priorização
- Métricas de sucesso por tipo de campanha
- Alocação de budget com justificativa

**Acionar com:** `/campaign-plan`

> **Fluxo recomendado:** use `/campaign-plan` para visão geral da campanha → use `/paid-traffic-management` para aprofundar a execução de mídia paga → use este agente para consultar dados reais da API Google Ads durante e após a campanha.

### `/05-google-analise-campanha`
Análise profunda de campanhas Google Ads com foco em diagnóstico de Quality Score, search terms e estrutura de keywords. Use quando o usuário precisar de:
- Diagnóstico de Quality Score por keyword (regra: QS > 7 não pausar / QS < 4 pausar imediatamente)
- Análise de search terms (termos que acionam os anúncios)
- Performance separada por network: Search, Display, YouTube, Shopping, PMax
- Identificação de problemas como baixo Impression Share, alto CPC, baixa conversão
- Recomendações acionáveis de otimização estrutural

**Benchmarks por network:**
- Search: CTR alvo 4–5%, QS alvo ≥ 7
- Display: CTR alvo 0,5–1,5%, foco em CPM e Conv Rate
- YouTube: foco em View Rate e CPV
- Shopping: CTR alvo 3–5%, ROAS alvo 2,5–4x
- PMax: foco em ROAS e Impression Share

**Acionar com:** `/05-google-analise-campanha`

### `/06-google-relatorio`
Geração de relatórios executivos Google Ads consolidados e por network. Use quando o usuário precisar de:
- Relatório executivo completo (10–12 páginas) com performance consolidada
- Performance separada por network (Search, Display, YouTube, Shopping, PMax)
- Análise de keywords top performers e underperformers
- Comparação período-a-período com variações percentuais
- Insights estratégicos e recomendações priorizadas

**Acionar com:** `/06-google-relatorio`

### `/07-google-copy`
Criação de copy otimizado para Google Ads em todos os formatos. Use quando o usuário precisar de:
- RSA (Responsive Search Ads): até 15 headlines (30 chars) e 4 descriptions (90 chars)
- Extensões: Sitelink, Call, Promotion, Structured Snippets
- Display Ads: headlines e descrições para banner
- YouTube Ads: script para Skippable In-Stream
- Variações A/B estruturadas para teste
- Templates por contexto: e-commerce, curso/educação, B2B/SaaS

**Acionar com:** `/07-google-copy`

> **Fluxo completo recomendado:** `/campaign-plan` (estratégia) → `/paid-traffic-management` (planejamento de mídia) → **agente API** (dados reais) → `/05-google-analise-campanha` (diagnóstico) → `/07-google-copy` (otimização de copy) → `/06-google-relatorio` (relatório executivo)

---

## Como gerar o Refresh Token (primeira vez)

1. Acesse o **Google Cloud Console** → crie um projeto e habilite a **Google Ads API**
2. Crie credenciais OAuth2 (tipo: "Desktop app") — copie `client_id` e `client_secret`
3. Acesse o **OAuth2 Playground** (https://developers.google.com/oauthplayground)
4. Em Settings → marque "Use your own OAuth credentials" e preencha client_id e client_secret
5. No campo de scope, cole: `https://www.googleapis.com/auth/adwords`
6. Clique "Authorize APIs" → faça login com a conta Google Ads
7. Clique "Exchange authorization code for tokens" → copie o `refresh_token`
