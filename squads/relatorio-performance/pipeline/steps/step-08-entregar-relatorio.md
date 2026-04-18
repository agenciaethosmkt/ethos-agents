---
step: "08"
name: "Entregar Relatório"
type: agent
agent: analista
condition: "checkpoint aprovar-relatorio aprovado"
---

# Step 08 — Entregar Relatório ao Cliente

## Após aprovação de Renato

### 1. Postar relatório completo como comentário na task

```
clickup_create_task_comment(task_id,
  "{conteúdo completo de output/relatorio.md}",
  notify_all=true
)
```

### 2. Verificar se há Google Drive configurado para o cliente

Se `custom_fields["Google Drive Cliente"]` estiver preenchido:
```
mcp__claude_ai_Google_Drive__create_file(
  name="Relatório Performance {cliente} — {período}",
  content="{conteúdo de output/relatorio.md}",
  parent_folder_id="{id da pasta do cliente}"
)
```

### 3. Atualizar status e campos da task

```
clickup_update_task(task_id,
  status="Concluído",
  custom_fields={"Último Relatório": "{data_hoje}"}
)
clickup_update_task(task_id, remove_assignees=[101151431])
```

### 4. Marcar tag de idempotência

```
clickup_add_tag_to_task(task_id, tag="agente-relatorio-processado")
```

### 5. Comentário de encerramento

```
clickup_create_task_comment(task_id,
  "📊 Relatório de performance entregue.\n\n**Cliente:** {cliente}\n**Período:** {data_inicio} a {data_fim}\n**Plataformas:** {plataformas}\n\nRelatório disponível nos comentários acima e na pasta do cliente no Drive (se configurado).")
```

## Registrar na memória do squad

Salvar em `_memory/runs.md`:
```
## {data_hoje} — {cliente} — {período}
- Plataformas: {meta | google | ambos}
- Campanhas analisadas: {quantidade}
- Principal insight: {resumo em 1 linha}
- Status: entregue
```
