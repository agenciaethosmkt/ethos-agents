---
step: "05"
name: "Entregar Diagnóstico"
type: agent
agent: analista-comercial
execution: inline
depends_on: step-04
---

# Step 05 — Analista Comercial: Entregar Diagnóstico

## Para o Pipeline Runner

O Analista Comercial posta o Raio X aprovado na descrição da task e avisa no comentário.

## Parte A — Atualizar descrição da task com o diagnóstico completo

```
clickup_update_task(task_id,
  description = [conteúdo completo de output/diagnostico.md]
)
```

Formatar em markdown legível no ClickUp:
- Negrito para títulos de seção: `**1. Situação Atual**`
- Tabelas para análise do funil e benchmarks
- Destaque em negrito para os 3 principais gargalos
- Separadores entre seções (`---`)

## Parte B — Comentar aviso de conclusão

```
clickup_create_task_comment(task_id,
  "🔍 Raio X de Vendas — [Empresa] — concluído.\n\n
  ▸ Gargalos identificados: [resumo dos 3 principais em 1 linha cada]\n
  ▸ Oportunidade estimada: R$ X/mês adicional\n
  ▸ Solução recomendada: [serviços]\n\n
  Diagnóstico completo na descrição desta task.\n
  ✅ Aguardando aprovação para montar proposta comercial.")
```

## Parte C — Atualizar status

```
clickup_update_task(task_id, status="em revisão")
```

## Parte D — Atualizar memória

Registrar em `_memory/memories.md`:
- Nome da empresa e segmento
- Principais gargalos identificados
- Solução recomendada
- Se converteu em proposta (atualizar em execução futura)
