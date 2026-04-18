---
step: "02"
name: "Processar Planilha de Leads"
type: agent
agent: analista
outputFile: output/dados-leads.md
---

# Step 02 — Processar Planilha de Leads do Cliente

## Padrão de arquivo no Drive

Cada cliente tem uma planilha com nome padrão: `[CLIENTE] - LEADS`

Estrutura conhecida:
- Aba **LEADS**: Data, Nome, Canal, Ponto de Contato, Serviço, Status, Valor da Venda, Objeção
- Aba **RESUMO**: DATA, SERVIÇO, VALOR, TOTAL DE VENDAS, TOTAL EM R$
- Aba **CONVERSÃO OFFLINE**: Data, e-mail, phone, value, currency

## Buscar planilha

```
mcp__claude_ai_Google_Drive__search_files(
  query="title contains '{cliente_nome}' and title contains 'LEADS'"
)
→ se encontrar: mcp__claude_ai_Google_Drive__read_file_content(file_id)
```

Tentar também: `title contains '{cliente_nome}' and mimeType = 'application/vnd.google-apps.spreadsheet'`

## Calcular métricas da planilha de leads

A partir da aba LEADS, calcular:

```python
total_leads         = contar todas as linhas com data
leads_fechados      = contar Status == "Negocio Fechado"
leads_perdidos      = contar Status == "Perdido" ou "Sem Retorno"
leads_em_aberto     = total_leads - leads_fechados - leads_perdidos
taxa_conversao      = leads_fechados / total_leads * 100

# Da aba RESUMO:
total_vendas        = campo "TOTAL DE VENDAS"
receita_total       = campo "TOTAL EM R$" (somar todos os valores)
ticket_medio        = receita_total / total_vendas

# Por canal:
leads_google        = contar Canal == "Google Ads"
leads_meta          = contar Canal == "Meta" ou "Facebook" ou "Instagram"
leads_organico      = contar Canal == "Orgânico" ou sem canal
```

## Identificar período dos dados

```
data_primeiro_lead = primeira data na planilha
data_ultimo_lead   = última data na planilha
periodo_planilha   = data_primeiro_lead → data_ultimo_lead
```

## Output — salvar em output/dados-leads.md

```markdown
# Dados de Leads — [Cliente] — [Período]

## Volume
- Total de leads: [X]
- Negócios fechados: [X] ([%] de conversão)
- Perdidos/sem retorno: [X]
- Em aberto: [X]

## Receita
- Total de vendas: [X] negócios
- Receita total: R$ [valor]
- Ticket médio: R$ [valor]

## Por canal
- Google Ads: [X] leads
- Meta Ads: [X] leads
- Orgânico: [X] leads

## Período dos dados
[data_primeiro_lead] → [data_ultimo_lead]

## Arquivo fonte
[nome da planilha] — [link do Drive]
```

## Se planilha não encontrada

Registrar ausência e continuar. O case será construído apenas com dados de campanha.
```
clickup_create_task_comment(task_id,
  "⚠️ Planilha de leads não encontrada no Drive para {cliente_nome}. Case será gerado apenas com dados de campanha.")
```
