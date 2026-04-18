---
step: "09"
name: "Entrega no ClickUp"
type: agent
agent: estrategista
execution: inline
depends_on: step-08
outputFile: output/entrega.md
---

# Step 09 — Entrega no ClickUp

## Para o Pipeline Runner

O Estrategista compila tudo e entrega na task do ClickUp que acionou o squad.

## Inputs

- `output/copy.md` — copy aprovado
- `output/design-canva-url.md` — links dos designs no Canva
- `output/revisao-final.md` — checklist de qualidade

## Processo

### 1. Postar comentário na task de origem

```
clickup_create_task_comment(task_id,
  "✅ Criativo entregue pelo squad Fábrica de Criativos.\n\n
  **Copy (Ogilvy):**\n[resumo das variações]\n\n
  **Design (Canva):**\n[links das variações]\n\n
  **Revisão:** [status da checklist]\n\n
  📋 Próximos passos: revisar os links acima, aprovar e subir no Gerenciador de Anúncios.",
  notify_all=true
)
```

### 2. Atualizar status da task

```
clickup_update_task(task_id, status="em revisão")
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```

### 3. Se chamado pelo Sobral (task_campanha_id preenchida no briefing)

Postar também na task de campanha linkada:
```
clickup_create_task_comment(task_campanha_id,
  "🎨 Criativos produzidos pela Fábrica de Criativos.\n[links Canva]\nAguardando aprovação para subir no Gerenciador.")
```

### 4. Registrar no log de execuções

```
clickup_create_task(
  list_name="Agente: Log de Execuções",
  name="Fábrica de Criativos — {cliente} — {produto}",
  description="task_id: {task_id}\nsquad: criativo-ads\nângulo: {angulo}\ncopy: {variações}\ndesign: {links}\nstatus: sucesso\ntimestamp: {ISO datetime}"
)
```

## Output esperado

Salvar em `output/entrega.md` o resumo completo da entrega com todos os links e status.
