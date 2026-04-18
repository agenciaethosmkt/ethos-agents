---
step: "01"
name: "Detectar Fase"
type: agent
agent: analista-comercial
---

# Step 01 — Detectar Fase e Verificar Idempotência

## Verificar idempotência por fase

```
clickup_get_task(task_id) → verificar tags
```

| Tag presente | Fase atual | Ação |
|---|---|---|
| `agente-crm-qualificacao` | qualificacao | PARAR — já processado |
| `agente-crm-followup` | followup | PARAR — já processado |
| `agente-crm-fechamento` | fechamento | PARAR — já processado |
| `agente-crm-renovacao` | renovacao | PARAR — já processado |

Se tag da fase atual já presente → parar. Não reprocessar.

## Detectar fase pelo status da task

```
task.status → fase
```

| Status | Fase |
|---|---|
| `qualificação` | qualificacao |
| `follow up` | followup |
| `negócio fechado` | fechamento |
| `para renovar` (lista Renovação) | renovacao |

## Se status não mapeado

```
clickup_create_task_comment(task_id,
  "⚠️ Status '{status}' não mapeado no squad follow-up-crm. Nenhuma ação executada.")
```
Não alterar nada. Abortar.

## Extrair dados básicos da task

```
clickup_get_task(task_id) → registrar:
- lead_nome = task.name ou custom_fields["Nome"]
- lead_empresa = custom_fields["Empresa"]
- lead_canal = custom_fields["Canal de Origem"]
- lead_plano = custom_fields["Plano de Interesse"]
- lead_orcamento = custom_fields["Orçamento"]
- historico = task.description
- reuniao_notas = task.comments (filtrar comentários relevantes)
```

Passar todos esses campos para o step da fase detectada.
