---
step: "06"
name: "Revisar Case"
type: agent
agent: analista
inputFile: output/case.md
---

# Step 06 — Gate de Qualidade + Checkpoint para Renato

## Checklist interno (antes de enviar para Renato)

- [ ] Todos os números batem com output/metricas.md
- [ ] Nenhum dado inventado ou estimado sem aviso
- [ ] Cliente anonimizado (padrão: segmento + cidade)
- [ ] Período curto (< 4 semanas) está sinalizado como "resultados iniciais"
- [ ] Se NPS ausente: seção de faturamento antes/depois omitida
- [ ] Narrativa legível por prospect não-técnico (sem jargão de mídia)
- [ ] "1 frase de destaque" presente e com número concreto

## Postar para revisão de Renato

```
clickup_create_task_comment(task_id,
  "📋 Case gerado — aguardando revisão.\n\n{conteúdo de output/case.md}\n\n---\n**Para aprovar:** confirme se pode usar o nome do cliente ou mantemos anônimo.\n**Para ajustar:** edite acima ou solicite reescrita.",
  notify_all=true
)
clickup_update_task(task_id, status="Em Revisão")
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```
