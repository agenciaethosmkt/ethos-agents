---
step: "07"
name: "Revisar Relatório"
type: agent
agent: revisor
inputFile: output/relatorio.md
---

# Step 07 — Revisor: Gate de Qualidade do Relatório

## Checklist obrigatório

### Dados
- [ ] Todos os números conferem com output/dados-meta.md e output/dados-google.md
- [ ] Nenhuma métrica inventada ou estimada sem aviso explícito
- [ ] Período correto indicado no cabeçalho
- [ ] Plataformas corretas listadas

### Linguagem
- [ ] Jargões técnicos explicados na primeira menção
- [ ] Nenhum campo vazio na tabela de resultados principais
- [ ] Tom adequado para cliente não-técnico
- [ ] Recomendações são ações concretas (não genéricas)

### Completude
- [ ] Resumo do período presente
- [ ] Pelo menos 2 destaques positivos
- [ ] Pelo menos 1 ponto de atenção (mesmo que o período tenha sido bom)
- [ ] Próximos passos definidos com responsável
- [ ] Tabela de dados detalhados preenchida

### Consistência
- [ ] O que "funcionou bem" é coerente com os dados brutos
- [ ] As recomendações são coerentes com os pontos de atenção
- [ ] Não há contradições entre o resumo e os dados detalhados

## Se reprovar

Devolver ao Redator com feedback específico:
```
❌ Reprovado — itens a corrigir:
1. [item específico]
2. [item específico]
```

## Se aprovar

Postar comentário na task do ClickUp:
```
clickup_create_task_comment(task_id,
  "✅ Relatório revisado e aprovado internamente.\n\nAguardando revisão final de Renato antes do envio ao cliente.")
clickup_update_task(task_id, status="Em Revisão")
clickup_update_task(task_id, add_assignees=[task.creator.id])
```

Avançar para checkpoint de aprovação de Renato.
