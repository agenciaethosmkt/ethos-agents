---
step: "05"
name: "Entregar Copy"
type: agent
agent: ogilvy
execution: inline
condition: "fase == copy"
---

# Step 05 — Ogilvy: Entregar Copy no ClickUp

## Para o Pipeline Runner

Ogilvy preenche os campos da task e move para revisão humana (Renato).

## Processo

### 1. Preencher campo "Legenda" da task

```
clickup_update_task(task_id,
  custom_fields={"Legenda": "{copy final de output/copy.md}"}
)
```

Para formatos longos (roteiro de Reels, e-mail, script):
```
clickup_update_task(task_id,
  description="{conteúdo completo de output/copy.md}"
)
```

### 2. Atualizar status para "Em Revisão"

```
clickup_update_task(task_id, status="Em Revisão")
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```

### 3. Postar comentário de entrega

```
clickup_create_task_comment(task_id,
  "✍️ Copy entregue pelo Ogilvy.\n\n**Formato:** {formato}\n**Objetivo:** {objetivo}\n\nRevisão de Renato necessária antes de avançar para design.",
  notify_all=true
)
```

> **Nota:** Após a aprovação de Renato, a automação do ClickUp moverá a task
> automaticamente para "Processo de Design & Criação", onde o agente será
> acionado novamente (Fase B).
