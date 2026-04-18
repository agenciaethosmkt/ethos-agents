# Step 05 — Devolver para Revisão

## Agente
analista-setup

## Objetivo
Mudar o status da task do marco ativado e da tarefa principal para "em revisão".

## Ações

```
# Task do marco que disparou
clickup_update_task(
  task_id=marco_ativado.task_id_marco,
  status="em revisão"
)

# Tarefa principal do projeto
clickup_update_task(
  task_id=projeto_id,
  status="em revisão"
)
```

## Registrar no log

```
clickup_create_task(
  list_id=LOG_LIST_ID,
  name="[Falconi] Acompanhamento — {projeto.cliente} [{marco_ativado.nome}]",
  description="Data: {hoje}\nMarco: {marco_ativado.nome}\nProjeto: {projeto.nome}\nStatus: {varredura.resumo}"
)
```

## Veto Conditions

Se o status atual da task já for "em revisão" → não alterar, apenas registrar no log.

## Output
Tasks atualizadas. Execução concluída.
