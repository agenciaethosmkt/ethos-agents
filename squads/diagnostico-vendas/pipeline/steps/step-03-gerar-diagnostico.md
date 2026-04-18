---
step: "03"
name: "Gerar Diagnóstico"
type: agent
agent: analista-comercial
execution: inline
depends_on: step-02
outputFile: output/diagnostico.md
---

# Step 03 — Analista Comercial: Gerar Diagnóstico

## Para o Pipeline Runner

Com briefing (step-01) e contexto de mercado (step-02), o Analista Comercial
monta o Raio X completo do prospect. Skills principais: `37-negocios-diagnostico`,
`30-marketing-funil`, `42-negocios-forecasting`.

## Estrutura do diagnóstico

### 1. Situação atual
Consolidar os dados do briefing em um parágrafo claro e objetivo.
Incluir: faturamento, ticket médio, taxa de conversão, canais, equipe, tempo de mercado.

### 2. Análise por etapa do funil
Para cada etapa, avaliar: situação atual, problema identificado, impacto no negócio.

Consultar `pipeline/data/funil-etapas.md` para as definições de cada etapa.

| Etapa | Situação | Problema identificado | Impacto |
|-------|----------|----------------------|---------|
| Atração | | | |
| Qualificação | | | |
| Proposta | | | |
| Fechamento | | | |
| Pós-venda / Retenção | | | |

### 3. Diagnóstico dos gargalos (ordenar por impacto)
Identificar os 3 principais gargalos que explicam o gap entre a situação atual e o objetivo.
Cada gargalo deve ter:
- Descrição clara do problema
- Causa raiz (não apenas o sintoma)
- Impacto estimado em receita (R$ ou % de conversão)

### 4. Benchmarks (usar output/contexto.md)
Comparar as métricas do prospect com os benchmarks do setor.
Destacar onde o prospect está abaixo da média — esses são os pontos de maior oportunidade.

### 5. Projeção de oportunidade
Com base nos gargalos e benchmarks, calcular o potencial de crescimento se os gargalos
forem resolvidos. Skill: `42-negocios-forecasting`.

Exemplo de estrutura:
- Situação atual: R$ X/mês
- Se taxa de conversão chegar ao benchmark: R$ X+Y/mês
- Se ticket médio aumentar X%: R$ X+Z/mês
- Potencial total endereçável: R$ X/mês (+X%)

### 6. Recomendação de solução Ethos
Consultar `pipeline/data/solucoes-ethos.md` e recomendar os serviços mais adequados
aos gargalos identificados. Justificar cada recomendação conectando ao gargalo específico.

Nunca recomendar mais de 3 serviços na primeira conversa — foco no gargalo principal.

### 7. Próximos passos sugeridos
Propor 2–3 ações concretas para o prospect, com prazo e responsável.
Sempre incluir: "Apresentar proposta comercial com base neste diagnóstico."

## Output esperado

Salvar em `output/diagnostico.md` seguindo a estrutura completa do Raio X definida
em `pipeline/data/funil-etapas.md`. Usar o template completo sem omitir seções.
