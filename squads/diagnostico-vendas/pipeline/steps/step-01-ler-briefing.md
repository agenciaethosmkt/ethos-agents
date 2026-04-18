---
step: "01"
name: "Ler Briefing do Diagnóstico"
type: agent
agent: analista-comercial
execution: inline
outputFile: output/briefing.yaml
---

# Step 01 — Analista Comercial: Ler Briefing do Diagnóstico

## Para o Pipeline Runner

O Analista Comercial lê todos os campos da task para montar o perfil do prospect/cliente
antes de qualquer análise ou pesquisa.

## Campos a extrair (task.custom_fields + task.description)

| Campo | Onde buscar | Obrigatório |
|---|---|---|
| `empresa` | Custom field "Empresa" ou título da task | ✅ |
| `segmento` | Custom field "Segmento" ou descrição | ✅ |
| `faturamento_atual` | Custom field "Faturamento Atual" ou descrição | ✅ |
| `objetivo` | Custom field "Objetivo" ou descrição | ✅ |
| `principal_gargalo` | Custom field "Gargalo" ou descrição | ✅ |
| `canais_aquisicao` | Descrição ou campo livre | ⚠️ opcional |
| `ticket_medio` | Custom field "Ticket Médio" ou descrição | ⚠️ opcional |
| `taxa_conversao` | Descrição | ⚠️ opcional |
| `equipe_vendas` | Descrição | ⚠️ opcional |
| `orcamento_marketing` | Custom field "Orçamento" | ⚠️ opcional |
| `tempo_no_mercado` | Descrição | ⚠️ opcional |
| `concorrentes` | Descrição ou campo livre | ⚠️ opcional |

## Verificar memória

Ler `_memory/memories.md` para checar se este prospect/cliente já passou pelo Raio X antes.
Se sim: registrar diferenças entre a situação anterior e a atual.

## Se campos obrigatórios ausentes

```
clickup_update_task(task_id, status="em alteração & ajustes")
clickup_create_task_comment(task_id,
  "🔍 Raio X não iniciado — campos ausentes:\n▸ [campo]: [onde preencher]\n\nPreencha e reenvie para o agente.")
```
→ ABORTAR

## Output esperado

Salvar em `output/briefing.yaml`:

```yaml
empresa: ""
segmento: ""
faturamento_atual: ""
objetivo: ""
principal_gargalo: ""
canais_aquisicao: []
ticket_medio: ""
taxa_conversao: ""
equipe_vendas: ""
orcamento_marketing: ""
tempo_no_mercado: ""
concorrentes: []
historico_ethos: ""    # já foi cliente? já fez diagnóstico antes?
```
