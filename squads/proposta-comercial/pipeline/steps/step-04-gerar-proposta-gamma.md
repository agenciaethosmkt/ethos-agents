---
step: "04"
name: "Entregar Conteúdo da Proposta"
type: agent
agent: analista-comercial
inputFile: output/conteudo-proposta.md
---

# Step 04 — Entregar Conteúdo da Proposta no ClickUp

## Objetivo

Postar o conteúdo estruturado da proposta na task do lead para que Renato monte visualmente no modelo de apresentação.

## 1. Postar conteúdo completo como comentário

```
clickup_create_task_comment(task_id,
  "📋 Proposta gerada — pronta para montar na apresentação.\n\n{conteúdo completo de output/conteudo-proposta.md}",
  notify_all=true
)
```

## 2. Criar documento no ClickUp para fácil acesso

```
clickup_create_document(
  name="Proposta — {lead_nome} — {plano} — {mes_ano}",
  parent_id="90170774473"  # Space Comercial
)
→ clickup_create_document_page(
  doc_id,
  title="Conteúdo da Proposta",
  content="{conteúdo de output/conteudo-proposta.md}"
)
```

## 3. Linkar documento na task

```
clickup_add_task_link(task_id, doc_id)
```

## 4. Atualizar status e assignees

```
clickup_update_task(task_id, status="Em Revisão")
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```

## 5. Comentário de instrução para Renato

```
clickup_create_task_comment(task_id,
  "✅ Conteúdo da proposta pronto.\n\n**Próximo passo:** montar na apresentação usando o modelo em:\nhttps://drive.google.com/drive/u/1/folders/1k7xllC9e6s_r-XQewiR_mQpG-ZZbadgK\n\nApós montar, aprovar aqui para registrar o envio.",
  notify_all=false
)
```
