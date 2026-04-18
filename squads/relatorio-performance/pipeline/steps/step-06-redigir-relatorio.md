---
step: "06"
name: "Redigir Relatório"
type: agent
agent: redator
inputFile: output/analise.md
outputFile: output/relatorio.md
---

# Step 06 — Redigir Relatório para o Cliente

## Objetivo

Transformar a análise técnica em um documento que o cliente entenda e confie. Tom: parceiro estratégico, não planilha de TI.

## Estrutura do relatório (para o cliente)

```markdown
# Relatório de Performance — [Nome do Cliente]
**Período:** {DATA_INICIO} a {DATA_FIM}
**Plataformas:** {Meta Ads | Google Ads | Ambos}
**Gerado em:** {data_hoje}

---

## Resumo do Período

[2–3 parágrafos em linguagem acessível:
- O que foi feito/rodado no período
- Principal resultado alcançado
- Uma frase de contexto sobre o mercado/sazonalidade se relevante]

---

## Resultados Principais

| Indicador | Resultado | Meta | Status |
|---|---|---|---|
| Investimento total | R$ {valor} | R$ {meta} | ✅/⚠️/❌ |
| Leads gerados | {qtd} | {meta} | ✅/⚠️/❌ |
| CPL (custo por lead) | R$ {valor} | R$ {meta} | ✅/⚠️/❌ |
| Alcance total | {qtd pessoas} | — | — |
| Cliques totais | {qtd} | — | — |

---

## O que funcionou bem

[2–3 bullets com dado + interpretação simples]
- **[Nome da campanha/criativo]**: [resultado] — [o que isso significa em termos de negócio]

---

## O que precisa de ajuste

[2–3 bullets com dado + causa + solução proposta]
- **[Ponto de atenção]**: [dado observado] — [causa provável] — [recomendação]

---

## Próximos Passos Recomendados

1. [ação concreta] — responsável: [Ethos | Cliente | Ambos]
2. [ação concreta] — responsável: [...]
3. [ação concreta] — responsável: [...]

---

## Dados Detalhados por Campanha

[tabela completa — para quem quiser aprofundar]

---

*Relatório gerado pela Ethos Marketing. Dúvidas? Entre em contato com seu gestor de conta.*
```

## Regras de linguagem

- **Nunca usar**: "CTR", "CPM", "impressões", "frequência" sem explicar entre parênteses
- **Usar**: "taxa de clique (CTR)", "custo por mil exibições (CPM)"
- **Tom**: direto, positivo mas honesto — não esconder problemas, contextualizar
- **Métricas sem meta**: apresentar o resultado e indicar se está dentro da média do setor
- **Sem jargão técnico desnecessário**: o cliente é empresário, não gestor de tráfego

## Feedback loop

Se for uma segunda iteração (Renato reprovou e devolveu), ler os comentários de feedback no início do output/relatorio.md e aplicar as correções solicitadas.
