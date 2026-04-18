# Step 01 — Ler Marco Ativado

## Agente
analista-setup

## Objetivo
Identificar qual marco foi ativado e localizar a tarefa principal do projeto.

## Inputs
- `task_id` — ID da task que disparou o RemoteTrigger

## Ações

```
clickup_get_task(task_id, subtasks=false)
```

Extrair:
- `task.name` — nome da task do marco
- `task.list.name` — nome da lista (identifica o marco: Kickoff / Ativação / Monitoramento)
- `task.custom_fields` — campos de relacionamento com a tarefa principal do projeto
- `task.status` — status atual
- `task.due_date` — data de vencimento
- `task.assignees` — responsáveis

## Identificação do Marco

| Lista | Marco |
|---|---|
| `[Connect] [1] Kickoff` | Marco 1 — Kickoff |
| `[Connect] [2] Ativação e Testes` | Marco 2 — Ativação |
| `[Connect] [3] Monitoramento e Otimização` | Marco 3 — Monitoramento |
| `[Flow] [1] Implementação [Kickoff]` | Marco 1 — Kickoff |
| `[Flow] [2] Ativação & Testes` | Marco 2 — Ativação |
| `[Flow] [3] Validação & Escala` | Marco 3 — Validação |
| `[Growth] [1] [Implementação] [Kickoff]` | Marco 1 — Kickoff |
| `[Growth] [2] [Ativação & Testes]` | Marco 2 — Ativação |
| `[Growth] [3] [Validação & Escala]` | Marco 3 — Validação |

## Localizar Tarefa Principal

O campo `[Connect/Flow/Growth] [N] [Marco]` do tipo `list_relationship` na task de marco aponta para a tarefa principal em **Painel de Projetos**.

Se o campo de relacionamento com o projeto não estiver preenchido → abortar com comentário:
> "⚠️ Falconi: não consegui identificar a tarefa principal deste projeto. Verifique o campo de relacionamento nesta task."

## Output
```
marco_ativado:
  tipo: "1 | 2 | 3"
  nome: "[nome da lista]"
  produto: "Connect | Flow | Growth"
  task_id_marco: "[id da task ativada]"
  projeto_id: "[id da tarefa principal em Painel de Projetos]"
```
