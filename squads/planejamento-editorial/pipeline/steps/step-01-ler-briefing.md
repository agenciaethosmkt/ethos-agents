---
step: "01"
name: "Ler Briefing do Mês"
type: agent
agent: ogilvy
execution: inline
outputFile: output/briefing.yaml
---

# Step 01 — Ogilvy: Ler Briefing do Mês

## Para o Pipeline Runner

Ogilvy lê todos os campos da task para entender o planejamento editorial que deve ser gerado.

## Campos a extrair (task.custom_fields + task.description)

| Campo | Onde buscar | Obrigatório |
|---|---|---|
| `cliente` | Custom field "Cliente" | ✅ |
| `mes_referencia` | Custom field "Mês de Referência" ou título da task | ✅ |
| `volume_semanal` | Custom field "Volume Semanal" ou descrição | ✅ |
| `pilares` | Custom field "Pilares de Conteúdo" ou descrição | ✅ |
| `objetivo_mes` | Custom field "Objetivo do Mês" ou descrição | ✅ |
| `tom_voz` | Custom field "Tom de Voz" | ⚠️ opcional |
| `restricoes` | Custom field "Restrições / Datas Importantes" | ⚠️ opcional |
| `referencias` | Descrição ou tasks linkadas | ⚠️ opcional |

## Verificar memória de execuções anteriores

Ler `_memory/memories.md` e verificar se há preferências anteriores do cliente:
- formatos preferidos
- pilares com melhor performance
- restrições conhecidas
- datas recorrentes (lançamentos, promoções sazonais)

## Se campos obrigatórios ausentes

```
clickup_update_task(task_id, status="em alteração & ajustes")
clickup_create_task_comment(task_id,
  "🔍 Planejamento não iniciado — campos ausentes:\n▸ [campo]: [onde preencher]\n\nPreencha e reenvie para o agente.")
```
→ ABORTAR

## Output esperado

Salvar em `output/briefing.yaml`:

```yaml
cliente: ""
mes_referencia: ""       # ex: "Maio 2026"
volume_semanal: 0        # posts por semana
total_posts: 0           # calculado: volume_semanal × semanas do mês
pilares: []              # lista de pilares
objetivo_mes: ""
tom_voz: ""
restricoes: ""           # datas bloqueadas, feriados, eventos especiais
referencias: ""
memoria_cliente: ""      # insights relevantes de _memory/memories.md
```
