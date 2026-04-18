---
step: "07"
name: "Publicar Case"
type: agent
agent: analista
condition: "checkpoint aprovar-case aprovado"
inputFile: output/case.md
---

# Step 07 — Publicar Case Aprovado

## 1. Salvar no Google Drive

Criar documento na pasta organizada por segmento:

```
mcp__claude_ai_Google_Drive__create_file(
  name="Case Ethos — {segmento} — {cliente_label} — {mes_ano}",
  content="{conteúdo de output/case.md}",
  mimeType="application/vnd.google-apps.document"
)
```

Pasta destino: buscar ou criar `/Cases Ethos/{segmento}/`

```
mcp__claude_ai_Google_Drive__search_files(
  query="title = 'Cases Ethos' and mimeType = 'application/vnd.google-apps.folder'"
)
```

## 2. Linkar na task do cliente em Gestão de Clientes

```
clickup_search(
  keywords="{cliente_nome}",
  filters={list: "Gestão de Clientes"}
)
→ clickup_create_task_comment(cliente_crm_id,
    "📊 Case documentado: {link_drive}\nPeríodo: {período}\nDestaques: {1 frase de resultado}")
```

## 3. Atualizar índice de cases para o squad proposta-comercial

Salvar em `_memory/cases-index.md`:

```markdown
## {segmento} — {cliente_label} — {mes_ano}
- Resultado destaque: {1 frase}
- Métricas: {leads X | conversão X% | CPL R$X | receita R$X}
- Plano: {Flow/Growth}
- Drive: {link}
- NPS disponível: {sim/não}
```

## 4. Finalizar task

```
clickup_add_tag_to_task(task_id, "agente-case-gerado")
clickup_update_task(task_id, status="Concluído")
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_create_task_comment(task_id,
  "✅ Case publicado e indexado.\n\n📁 Drive: {link_drive}\n🔗 Linkado na task do cliente em Gestão de Clientes.\n📋 Índice atualizado para uso no squad proposta-comercial.")
```
