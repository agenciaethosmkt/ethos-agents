---
step: "08"
name: "Entregar Design"
type: agent
agent: designer
execution: inline
condition: "fase == design"
---

# Step 08 — Designer: Entregar Design no ClickUp

## Processo

### 1. Anexar arquivos na task

```
clickup_attach_task_file(task_id, file_path="{caminho do PNG}")
```
Repetir para cada arquivo gerado.

### 2. Atualizar status para "Em Revisão"

```
clickup_update_task(task_id, status="Em Revisão")
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```

### 3. Postar comentário de entrega

```
clickup_create_task_comment(task_id,
  "🎨 Design entregue.\n\n**Formato:** {formato}\n**Arquivos:** {quantidade} arquivo(s) anexado(s)\n\nRevisão de Renato necessária. Após aprovação, a task seguirá para agendamento.",
  notify_all=true
)
```

> **Nota:** Após aprovação de Renato, a automação move a task para
> "Agendamentos, Publicações & Disparos" — onde o agente será acionado
> novamente (Fase C), EXCETO se for criativo de anúncio
> (esses vão para Laboratório de Criativos → squad criativo-ads).
