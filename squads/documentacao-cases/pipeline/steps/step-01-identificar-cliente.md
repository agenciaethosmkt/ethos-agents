---
step: "01"
name: "Identificar Cliente e Contexto"
type: agent
agent: analista
---

# Step 01 — Identificar Cliente e Contexto

## Extrair dados da task

```
clickup_get_task(task_id) → extrair:
- cliente_nome        → nome do cliente (campo custom "Cliente" ou task.name)
- cliente_segmento    → clínica / eletricista / outro
- plano_contratado    → Flow / Growth / outro
- data_inicio         → início do contrato
- data_fim_periodo    → fim do período a documentar (hoje se em curso)
- notas_extras        → observações de Renato na task (contexto adicional)
```

## Buscar task do cliente em Gestão de Clientes

```
clickup_search(
  keywords="{cliente_nome}",
  filters={list: "Gestão de Clientes"}
)
→ clickup_get_task(cliente_crm_id) → extrair:
  - faturamento, cidade, tempo de contrato, serviços contratados
  - credenciais (ID BM Meta, Token Meta, ID Google Ads) para busca na API
```

## Calcular período do case

```
periodo_meses = diferença em meses entre data_inicio e data_fim_periodo
periodo_label = "{mes/ano início} a {mes/ano fim}"
```

## Registrar contexto base

```markdown
# Contexto do Case — [Cliente]

- Segmento: [segmento]
- Plano: [plano]
- Período: [data_inicio] → [data_fim_periodo] ([X] meses)
- Faturamento declarado: R$ [valor]/mês
- Situação inicial (notas de Renato): [notas ou "não registrado"]
```
