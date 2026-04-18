# Step 06 — Passagem Interna para a Operação

**Persona:** Atendimento  
**Objetivo:** Notificar áreas envolvidas, finalizar a task e registrar no log.

## Inputs

- `cliente_nome`, `plano_contratado`, `areas_envolvidas`
- `doc_url` — link do documento de resumo do onboarding (Step 04)

## Execução

### 1. Comentário de conclusão na task

```
clickup_create_task_comment(task_id,
  "✅ Onboarding concluído — [data]\n\n" +
  "📋 Resumo: [doc_url]\n\n" +
  "🎯 Prioridades: [resumo em 2-3 linhas das prioridades do cliente]\n\n" +
  "⚠️ Riscos/travas: [se houver — caso contrário omitir]\n\n" +
  "📌 Próximos passos: briefing + acessos + setup encaminhados ao cliente\n\n" +
  "👥 Áreas acionadas: [lista]",
  notify_all=true
)
```

### 2. Áreas a notificar (por plano contratado)

| Área | C-Level | Quando acionar |
|---|---|---|
| Tráfego Pago | Sobral | Se plano inclui tráfego |
| Conteúdo / Social Media | Kizo | Se plano inclui conteúdo |
| Copy | Ogilvy | Se plano inclui copy |
| Financeiro / Jurídico | Falconi | Se pendências de contrato |

Criar subtask para cada área acionada com: cliente, plano, prioridades e link do doc de onboarding.

### 3. Finalizar a task

```
clickup_update_task(task_id, status="em revisão")
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```

### 4. Registrar no log

```
clickup_create_task(
  list_name="Agente: Log de Execuções",
  name="Jobs/sucesso-cliente — Onboarding {cliente_nome}",
  description="task_id: {task.id}\ncliente: {cliente_nome}\nplano: {plano_contratado}\nstatus: sucesso\ntimestamp: {ISO datetime}\nurl: {task.url}"
)
```

## Checklist de conclusão

```
[ ] Documento de resumo criado no ClickUp
[ ] Mensagem de agendamento gerada (Step 02)
[ ] Pauta da reunião preparada (Step 03)
[ ] Próximos passos enviados ao cliente (Step 05)
[ ] Áreas internas notificadas
[ ] Task finalizada: status em revisão, assignee → creator
[ ] Log registrado
```
