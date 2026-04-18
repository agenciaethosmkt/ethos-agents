---
step: "06"
name: "Entregar Follow-up"
type: agent
agent: redator
condition: "fase == followup"
inputFile: output/followup.md
---

# Step 06 — Entregar Follow-up Aprovado no ClickUp

## Após aprovação de Renato no checkpoint

### 1. Postar mensagem como comentário na task

```
clickup_create_task_comment(task_id,
  "✉️ Mensagem de follow-up pronta para envio.\n\n---\n{mensagem aprovada de output/followup.md}\n---\n\nEnviar via WhatsApp para {lead_nome}.",
  notify_all=true
)
```

### 2. Atualizar assignees

```
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```

### 3. Marcar tag de idempotência da fase

```
clickup_add_tag_to_task(task_id, "agente-crm-followup")
```

> **Nota:** O envio da mensagem é manual — Renato copia e envia via WhatsApp.
> O envio automático via Z-API pode ser configurado futuramente quando o fluxo estiver validado.
