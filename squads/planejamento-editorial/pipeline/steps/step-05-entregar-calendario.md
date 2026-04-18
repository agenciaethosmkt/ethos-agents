---
step: "05"
name: "Entregar Calendário"
type: agent
agent: ogilvy
execution: inline
depends_on: step-04
---

# Step 05 — Ogilvy: Entregar Calendário

## Para o Pipeline Runner

Ogilvy entrega o calendário aprovado no ClickUp: cria as tasks na Máquina de Ideias
e posta o resumo mensal como comentário na task-mãe.

## Parte A — Criar tasks na Máquina de Ideias

Para cada post do `output/calendario.md`, criar uma task:

```
clickup_create_task(
  list_id = "901701992020",  # Máquina de Ideias
  name = "[Formato] [Tema] — [Cliente]",
  description = gancho + objetivo + cta,
  due_date = data_do_post,
  custom_fields = {
    "Formato": formato,
    "Pilar de Conteúdo": pilar,
    "Objetivo": objetivo,
    "Cliente": cliente,
  }
)
```

### Regras de criação de tasks
- Nome: `[FORMATO] Tema do post — Cliente` (ex: `[CARROSSEL] Como escolher o plano certo — Cliente X`)
- Due date: data exata do post
- Não criar tasks para datas bloqueadas
- Se a task-mãe tiver task de campanha linkada, linkar também às tasks criadas

## Parte B — Comentar na task-mãe com resumo

```
clickup_create_task_comment(task_id,
  "📅 Calendário editorial de [Mês/Ano] gerado.\n\n
  ▸ Total de posts: X\n
  ▸ Formatos: X carrosseis, X reels, X feeds, X stories\n
  ▸ Pilares cobertos: [lista]\n
  ▸ [N] tasks criadas na Máquina de Ideias\n\n
  Calendário completo: [link para output/calendario.md ou resumo inline]\n\n
  ✅ Aguardando aprovação para iniciar produção.")
```

## Parte C — Atualizar status e memória

```
clickup_update_task(task_id, status="em revisão")
```

Salvar em `output/tasks-criadas.yaml`:
```yaml
mes: ""
cliente: ""
total_tasks: 0
tasks:
  - id: ""
    nome: ""
    data: ""
    formato: ""
    pilar: ""
```

Atualizar `_memory/memories.md` com:
- Volume planejado para o mês
- Distribuição de formatos e pilares escolhida
- Qualquer ajuste feito no checklist de revisão (aprendizado)
