---
step: "01"
name: "Ler Briefing do Reels"
type: agent
agent: ogilvy
execution: inline
outputFile: output/briefing.yaml
---

# Step 01 — Ogilvy: Ler Briefing do Reels

## Para o Pipeline Runner

Ogilvy lê todos os campos da task para entender o Reels que precisa ser roteirizado.

## Campos a extrair (task.custom_fields + task.description)

| Campo | Onde buscar | Obrigatório |
|---|---|---|
| `cliente` | Custom field "Cliente" | ✅ |
| `tema` | Custom field "Tema" ou título da task | ✅ |
| `objetivo` | Custom field "Objetivo" | ✅ |
| `duracao_alvo` | Custom field "Duração" ou descrição | ✅ |
| `pilar` | Custom field "Pilar de Conteúdo" | ✅ |
| `gancho_sugerido` | Descrição ou Custom field "Gancho" | ⚠️ opcional |
| `referencia_visual` | Descrição ou links anexados | ⚠️ opcional |
| `tom_voz` | Custom field "Tom de Voz" ou memória do cliente | ⚠️ opcional |
| `data_publicacao` | Custom field "Data de Publicação" | ⚠️ opcional |

## Verificar memória do cliente

Ler `_memory/memories.md` para identificar:
- Estilo de roteiro que funciona para o cliente
- Formatos de Reels com melhor performance
- Restrições de produção (sem voz off, sem texto longo na tela, etc.)

## Se campos obrigatórios ausentes

```
clickup_update_task(task_id, status="em alteração & ajustes")
clickup_create_task_comment(task_id,
  "🔍 Roteiro não iniciado — campos ausentes:\n▸ [campo]: [onde preencher]\n\nPreencha e reenvie para o agente.")
```
→ ABORTAR

## Output esperado

Salvar em `output/briefing.yaml`:

```yaml
cliente: ""
tema: ""
objetivo: ""             # awareness / engajamento / conversão / educação
duracao_alvo: ""         # ex: "30s", "45s", "60s"
pilar: ""
gancho_sugerido: ""      # vazio se não briefado
referencia_visual: ""
tom_voz: ""
data_publicacao: ""
memoria_cliente: ""      # insights de _memory/memories.md
```
