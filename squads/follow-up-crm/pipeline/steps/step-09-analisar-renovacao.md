---
step: "09"
name: "Analisar Histórico para Renovação"
type: agent
agent: analista-comercial
condition: "fase == renovacao"
outputFile: output/analise-renovacao.md
---

# Step 09 — Analisar Histórico do Cliente para Renovação

## Objetivo

Entender a jornada do cliente no contrato atual antes de redigir a abordagem de renovação. Renovação é mais fácil quando mostramos resultado — e mais difícil quando negligenciamos o relacionamento.

## Buscar dados do cliente ativo

```
clickup_get_task(task_id) → extrair:
- cliente_nome, plano_atual, valor_atual, data_inicio_contrato, data_vencimento
- custom_fields["Faturamento Atual"] (se atualizado)
```

Buscar task do cliente em Gestão de Clientes para histórico completo:
```
clickup_search(keywords="{cliente_nome}", filters={list: "Gestão de Clientes"})
→ clickup_get_task(cliente_crm_id) → ler campos e descrição
→ clickup_get_task_comments(cliente_crm_id) → histórico de relacionamento
```

## Buscar resultados de campanhas (se tráfego pago)

```
clickup_search(keywords="{cliente_nome}", filters={list: "Processo de Otimização"})
→ buscar último relatório de performance ou comentários de otimização
```

## Buscar transcrições de reuniões no Drive (Tactiq)

```
mcp__claude_ai_Google_Drive__search_files(query="tactiq {cliente_nome}")
→ ler transcrições relevantes para identificar: satisfação, reclamações, pedidos pendentes
```

## Avaliar saúde do relacionamento

| Indicador | Sinal positivo | Sinal de alerta |
|---|---|---|
| Resultados entregues | Metas atingidas ou superadas | Abaixo do esperado sem comunicação |
| Relacionamento | Contato frequente e positivo | Reclamações sem resolução |
| Engajamento | Participa, responde, envia materiais | Sumido, demora para responder |
| Ticket atual | Adequado ao resultado | Pode sentir que paga caro |

## Output — salvar em output/analise-renovacao.md

```markdown
# Análise de Renovação — [Cliente] — [Data]

## Contrato atual
- Plano: [plano]
- Valor: R$ [valor]/mês
- Duração: [início] → [vencimento]
- Meses restantes: [X]

## Histórico de resultados
[principais entregas e resultados do período]

## Saúde do relacionamento
- Nível de satisfação percebido: [alto / médio / baixo]
- Último contato registrado: [data e contexto]
- Reclamações ou pendências abertas: [lista ou "nenhuma"]

## Proposta para renovação
- Manter plano atual: R$ [valor]/mês
- Upgrade sugerido: [plano superior] — R$ [valor]/mês — justificativa: [motivo]
- Ajuste de valor (se necessário): [contexto]

## Tom recomendado para abordagem
[Celebrar resultados e propor continuidade / Reconhecer dificuldades e propor ajuste / Abordagem consultiva com upgrade]

## Alertas para Renato
[pontos de atenção antes da conversa de renovação]
```
