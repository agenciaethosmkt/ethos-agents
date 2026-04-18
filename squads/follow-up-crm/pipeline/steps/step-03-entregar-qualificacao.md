---
step: "03"
name: "Entregar Qualificação"
type: agent
agent: analista-comercial
condition: "fase == qualificacao"
inputFile: output/analise-lead.md
---

# Step 03 — Entregar Qualificação no ClickUp

## Ação baseada no score de fit

### Se score Alto ou Médio → avançar para reunião

```
clickup_create_task_comment(task_id,
  "🎯 Qualificação concluída.\n\n**Score de Fit:** {Alto/Médio}\n**ICP:** {Flow/Growth/Eletricistas/Novo público}\n**Faturamento:** R$ {valor}/mês\n\n**Análise:**\n{resumo da análise BANT}\n\n**Produto sugerido:** {produto}\n\n**Recomendação:** Avançar para reunião de diagnóstico.",
  notify_all=true
)
clickup_update_task(task_id,
  custom_fields={"Score de Fit": "{Alto/Médio}", "Produto Sugerido": "{produto}"}
)
```

### Se score Baixo (com possibilidade) → solicitar mais dados

```
clickup_create_task_comment(task_id,
  "⚠️ Qualificação incompleta — informações insuficientes para determinar fit.\n\n**Falta apurar:**\n{lista de informações}\n\n**Sugestão:** perguntar ao lead antes de agendar reunião.")
```

### Se sem fit → desqualificar

```
clickup_update_task(task_id, status="desqualificado")
clickup_create_task_comment(task_id,
  "❌ Lead desqualificado.\n\n**Motivo:** {motivo}\n\n**Ação tomada:** status atualizado para Desqualificado. Lead pode ser nutrido futuramente se perfil mudar.")
```

## Marcar tag de idempotência da fase

```
clickup_add_tag_to_task(task_id, "agente-crm-qualificacao")
```

## Remover Claude dos assignees

```
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```
