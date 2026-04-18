# Step 05 — Entregar no ClickUp

## Agente
desenvolvedor

## Objetivo
Postar o resultado na **descrição da task** e devolver para revisão humana.

## Ações

### 1. Atualizar descrição da task com a entrega

```
clickup_update_task(
  task_id=task.id,
  description=relatorio_entrega
)
```

### Formato da descrição de entrega

```
🌐 LaryPages — Entrega: {tipo_task}
{data_hoje}

━━━━━━━━━━━━━━━━━━━━━━━━
✅ O QUE FOI FEITO
{resumo do trabalho executado}

━━━━━━━━━━━━━━━━━━━━━━━━
📦 ENTREGÁVEIS
{lista de arquivos / links / docs gerados}

━━━━━━━━━━━━━━━━━━━━━━━━
📋 CHECKLIST TÉCNICO
{resultado do checklist do step-04}

━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ PONTOS DE ATENÇÃO (se houver)
{itens que precisam de revisão ou decisão humana}

━━━━━━━━━━━━━━━━━━━━━━━━
➡️ PRÓXIMOS PASSOS
{1-3 ações para o humano após revisão}
```

### 2. Atualizar status e assignee

```
clickup_update_task(task_id=task.id, status="em revisão")
clickup_update_task(task_id=task.id, remove_assignees=[101151431], add_assignees=[task.creator.id])
```

### 3. Registrar no log

```
clickup_create_task(
  list_id=LOG_LIST_ID,
  name="[LaryPages] {tipo_task} — {task.name}",
  description="Cliente: {cliente}\nTipo: {tipo_task}\nData: {hoje}\nStatus: entregue para revisão"
)
```

## Output
Descrição da task atualizada com a entrega. Task devolvida ao humano para aprovação.
