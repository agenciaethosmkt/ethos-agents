---
step: "11"
name: "Entregar Abordagem de Renovação"
type: agent
agent: analista-comercial
condition: "fase == renovacao"
inputFile: output/renovacao.md
---

# Step 11 — Entregar Abordagem de Renovação no ClickUp

## Após aprovação de Renato no checkpoint

### 1. Postar análise + mensagem como comentário

```
clickup_create_task_comment(task_id,
  "🔄 Análise de renovação concluída.\n\n**Saúde do relacionamento:** {saudável/atenção}\n**Proposta:** {manter/upgrade} — R$ {valor}/mês\n\n---\n**Mensagem sugerida (WhatsApp):**\n\n{mensagem aprovada}\n---\n\n**Notas para a conversa:**\n{notas para Renato}",
  notify_all=true
)
```

### 2. Atualizar campos da task

```
clickup_update_task(task_id,
  custom_fields={
    "Proposta de Renovação": "R$ {valor}/mês — {plano}",
    "Data da Abordagem": "{data_hoje}"
  }
)
```

### 3. Marcar tag de idempotência da fase

```
clickup_add_tag_to_task(task_id, "agente-crm-renovacao")
```

### 4. Remover Claude dos assignees

```
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```
