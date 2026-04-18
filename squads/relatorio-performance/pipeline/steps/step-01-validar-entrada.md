---
step: "01"
name: "Validar Entrada"
type: agent
agent: analista
---

# Step 01 — Validar Entrada

## Verificar idempotência

```
clickup_get_task(task_id) → verificar tags
Se tag "agente-relatorio-processado" presente → PARAR (já processado)
```

## Extrair campos obrigatórios

```
clickup_get_task(task_id) → extrair:
- custom_fields["Cliente"]           → nome do cliente
- custom_fields["Período"]           → data início e data fim do relatório
- custom_fields["Plataforma"]        → Meta Ads | Google Ads | Ambos
- custom_fields["ID BM Meta"]        → Business Manager ID (se Meta)
- custom_fields["Token Meta"]        → Token de acesso (se Meta)
- custom_fields["ID Cliente Google"] → Customer ID Google Ads (se Google)
- task.description                   → contexto adicional, objetivos da campanha
```

## Validação

| Campo | Obrigatório | Ação se ausente |
|---|---|---|
| Cliente | Sim | Comentar e abortar |
| Período | Sim | Usar últimos 30 dias como padrão, registrar no comentário |
| Plataforma | Sim | Comentar e abortar |
| Credenciais da plataforma | Sim | Buscar no ClickUp CRM antes de abortar |

## Se credenciais não encontradas na task

Buscar nos campos personalizados do cliente no CRM:
```
clickup_search(keywords="{nome_cliente}", filters={list: "Gestão de Clientes"})
→ clickup_get_task(cliente_task_id) → extrair credenciais
```

## Se abortar

```
clickup_create_task_comment(task_id,
  "⚠️ Relatório não iniciado — campos obrigatórios ausentes: {lista de campos}.\n\nPreencher e reabrir a task.")
```
Não marcar tag de processado. Não alterar status.
