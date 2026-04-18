# Regras Globais — Sistema Ethos Agentes

Este arquivo deve ser lido por **todos os agentes** no início de cada execução. As regras aqui definidas têm precedência sobre qualquer instrução nos arquivos de squad ou persona.

---

## 1. Identidade Claude no ClickUp

**Todo comentário postado via `clickup_create_task_comment` DEVE incluir `assignee: 101151431`.**

Este é o User ID do perfil Claude no workspace Ethos. Sem esse parâmetro, o comentário não será atribuído ao Claude.

```
clickup_create_task_comment(
  task_id    = "<id>",
  comment_text = "<texto>",
  assignee   = 101151431   ← OBRIGATÓRIO em todos os comentários
)
```

Isso se aplica a **todos os contextos**:
- Comentário de ativação (⚙️ Agente ativado...)
- Comentário de erro ou campo ausente
- Comentário de entrega ou resumo
- Comentário de revisão interna
- Qualquer outro comentário em qualquer squad

---

## 2. Entrega na descrição, resumo no comentário

- Conteúdo principal (copy, roteiro, relatório, diagnóstico) → `clickup_update_task(description=...)`
- Comentário com resumo de entrega → `clickup_create_task_comment(assignee=101151431, ...)`

Nunca entregar conteúdo longo via comentário.

---

## 3. Idempotência

Antes de executar qualquer squad, confirmar ausência da tag `agente-processado`. Se presente, encerrar sem ação.

---

## 4. Encerramento padrão

Ao concluir qualquer execução:
1. `clickup_update_task(task_id, status="em revisão")`
2. `clickup_update_task(task_id, remove_assignees=[101151431])`
3. `clickup_update_task(task_id, add_assignees=[task.creator.id])`
4. `clickup_create_task_comment(task_id, "✅ ...", assignee=101151431, notify_all=true)`
