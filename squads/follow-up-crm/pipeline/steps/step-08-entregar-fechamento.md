---
step: "08"
name: "Entregar Briefing e Registrar no CRM"
type: agent
agent: analista-comercial
condition: "fase == fechamento"
inputFile: output/briefing-cliente.md
---

# Step 08 — Registrar Novo Cliente no CRM e Disparar Onboarding

## 1. Atualizar campos da task do lead com dados consolidados

```
clickup_update_task(task_id,
  custom_fields={
    "Plano Contratado": "{plano}",
    "Valor Mensal": "{valor}",
    "Data de Início": "{data_inicio}",
    "Faturamento": "{faturamento}",
    "Segmento": "{segmento}"
  }
)
```

## 2. Postar briefing completo como comentário

```
clickup_create_task_comment(task_id,
  "🎉 Negócio fechado — briefing do cliente consolidado.\n\n{conteúdo de output/briefing-cliente.md}",
  notify_all=true
)
```

## 3. Verificar se Make já criou a task em Gestão de Clientes

A automação do Make cria automaticamente a task do cliente em `Comercial > CRM > Gestão de Clientes` quando o status muda para `negócio fechado`. Verificar se foi criada:

```
clickup_search(
  keywords="{lead_nome}",
  filters={list: "Gestão de Clientes"}
)
```

**Se já criada pelo Make:** atualizar com os campos consolidados do briefing.
**Se não criada ainda:** aguardar automação ou criar manualmente:

```
clickup_create_task(
  list_name="Gestão de Clientes",
  name="{lead_nome} — {lead_empresa}",
  description="{conteúdo de output/briefing-cliente.md}",
  custom_fields={...campos do briefing...}
)
```

## 4. Marcar tag de idempotência da fase

```
clickup_add_tag_to_task(task_id, "agente-crm-fechamento")
```

## 5. Sinalizar para onboarding

```
clickup_create_task_comment(task_id,
  "📋 Briefing registrado no CRM. Squad onboarding-cliente pode ser acionado para agendar a reunião de kickoff.",
  notify_all=false
)
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```
