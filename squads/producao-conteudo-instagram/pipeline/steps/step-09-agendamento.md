---
step: "09"
name: "Configurar Agendamento"
type: agent
agent: ogilvy
execution: inline
condition: "fase == agendamento"
---

# Step 09 — Agendamento e Publicação

## Para o Pipeline Runner

A peça chegou em "Agendamentos, Publicações & Disparos" aprovada por Renato.
Configurar o `due_date` correto para acionar o Make e publicar automaticamente.

## Inputs

```
clickup_get_task(task_id) → extrair:
- custom_fields["Data de Publicação"]   → data e hora da publicação
- custom_fields["Formato"]              → para identificar exceções manuais
```

## Regra do due_date

> ⚠️ O campo que aciona o Make é o **due_date**, não o start_date.
> (Exceção: lista "Envio de Mensagens" usa start_date — mas esta lista é diferente.)

```
clickup_update_task(task_id,
  due_date="{data_publicacao em timestamp ms}",
  status="Agendado"
)
```

## Exceções — publicação manual

| Formato | Motivo | Ação |
|---|---|---|
| Stories | Sem API de publicação automática | Comentar instruções manuais |
| Vídeo YouTube | Sem automação configurada | Comentar instruções manuais |

Para formatos manuais:
```
clickup_create_task_comment(task_id,
  "📋 Publicação manual necessária.\n\n**Formato:** {formato}\n**Data:** {data_publicacao}\n\nEste formato não tem automação — publicar manualmente no horário indicado.")
clickup_update_task(task_id, status="Agendado")
```

## Para formatos automatizados

```
clickup_create_task_comment(task_id,
  "⏰ Agendado para {data_publicacao}.\nMake publicará automaticamente no horário definido.")
clickup_update_task(task_id, remove_assignees=[101151431])
```
