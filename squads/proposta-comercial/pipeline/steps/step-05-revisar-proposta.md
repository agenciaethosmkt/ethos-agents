---
step: "05"
name: "Revisar Proposta"
type: agent
agent: analista-comercial
inputFiles:
  - output/conteudo-proposta.md
  - output/proposta-canva.md
---

# Step 05 — Gate de Qualidade da Proposta

## Checklist de conteúdo

### Personalização
- [ ] Nome do lead aparece pelo menos 3 vezes
- [ ] Hero menciona a dor específica do lead (não genérica)
- [ ] Diagnóstico usa palavras do próprio lead (da transcrição Tactiq ou formulário)
- [ ] Case de prova social é do mesmo segmento ou situação parecida

### Estrutura
- [ ] Proposta NÃO começa falando sobre a Ethos — começa com o lead
- [ ] Resultado esperado é específico e mensurável (com número e prazo)
- [ ] Pilares do método correspondem ao plano (ver `pipeline/data/pilares-por-plano.md`)
- [ ] Entregas batem com o escopo real do plano (ver `pipeline/data/planos-ethos.md`)
- [ ] Investimento está correto para o plano
- [ ] CTA presente com prazo de validade

### Tom
- [ ] Cada seção tem no máximo 60 palavras
- [ ] Números concretos presentes (sem adjetivos vagos)
- [ ] Ancoragem de valor antes do preço

## Se reprovar

```
❌ Reprovado — devolver ao Redator:
1. [item específico]
2. [item específico]
```

## Se aprovar

Postar no ClickUp para Renato revisar antes de enviar ao lead:

```
clickup_create_task_comment(task_id,
  "✅ Proposta pronta para revisão de Renato.\n\n📎 Design Canva: https://www.canva.com/design/{design_id}/edit\n\n**Para enviar ao lead:**\n1. Abrir o link e revisar\n2. Publicar como site no Canva (Compartilhar → Publicar como site)\n3. Aprovar aqui para registrar o envio",
  notify_all=true
)
clickup_update_task(task_id, status="Em Revisão")
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```
