---
step: "06"
name: "Registrar Envio da Proposta"
type: agent
agent: analista-comercial
condition: "checkpoint aprovar-proposta aprovado"
---

# Step 06 — Registrar Envio e Atualizar CRM

## Após aprovação de Renato

### 1. Registrar proposta enviada na task

```
clickup_create_task_comment(task_id,
  "📤 Proposta enviada ao lead.\n\n**Cliente:** {lead_nome}\n**Plano:** {plano}\n**Investimento:** R$ {valor}/mês\n**Link da proposta:** {link_canva_site}\n**Válida até:** {data_hoje + 7 dias}\n\nAguardando retorno do lead.",
  notify_all=true
)
```

### 2. Atualizar campos da task

```
clickup_update_task(task_id,
  status="follow up",
  custom_fields={
    "Data Envio Proposta": "{data_hoje}",
    "Validade Proposta": "{data_hoje + 7 dias}",
    "Plano Proposto": "{plano}",
    "Valor Proposto": "{valor}"
  }
)
```

### 3. Marcar tag de idempotência

```
clickup_add_tag_to_task(task_id, "agente-proposta-processado")
```

### 4. Remover Claude e devolver para Renato

```
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```

### 5. Registrar na memória do squad

Salvar em `_memory/runs.md`:
```
## {data_hoje} — {lead_nome} — {segmento} — task:{task_id}
- Plano: {plano}
- Valor: R$ {valor}/mês
- Case usado: {case}
- Status: proposta enviada
```

> **Nota:** Após o envio, o squad `follow-up-crm` assume o acompanhamento.
> A task irá para status "follow up" e o Concer acionará automaticamente
> o follow-up pós-proposta se o lead não responder.
