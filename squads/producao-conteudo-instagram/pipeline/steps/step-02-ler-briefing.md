---
step: "02"
name: "Ler Briefing"
type: agent
agent: ogilvy
execution: inline
condition: "fase == copy"
outputFile: output/briefing.yaml
---

# Step 02 — Ogilvy: Ler Briefing da Task

## Para o Pipeline Runner

O Ogilvy lê todos os campos da task para entender o que precisa ser produzido.

## Campos a extrair (task.custom_fields + task.description)

| Campo | Onde buscar | Obrigatório |
|---|---|---|
| `formato` | Custom field "Formato" | ✅ |
| `briefing` | Custom field "Briefing" | ✅ |
| `objetivo` | Custom field "Objetivo" | ✅ |
| `data_publicacao` | Custom field "Data de Publicação" | ✅ |
| `cliente` | Custom field "Cliente" | ✅ |
| `pilar` | Custom field "Pilar de Conteúdo" | ⚠️ opcional |
| `referencias` | Descrição ou campo | ⚠️ opcional |

## Identificar skill a usar por formato

Consultar `pipeline/data/skills-por-formato.md` e registrar qual skill será injetada no step-03.

## Se campos obrigatórios ausentes

```
clickup_update_task(task_id, status="em alteração & ajustes")
clickup_create_task_comment(task_id,
  "🔍 Copy não iniciada — campos ausentes:\n▸ [campo]: [onde preencher]\n\nPreencha e reenvie para o agente.")
```
→ ABORTAR

## Output esperado

Salvar em `output/briefing.yaml`:

```yaml
cliente: ""
formato: ""          # post-feed / carrossel / reels / stories / email / whatsapp
objetivo: ""
briefing: ""
data_publicacao: ""
pilar: ""
referencias: ""
skill: ""            # skill identificada para este formato
```
