---
step: "02"
name: "Pesquisar Contexto e Setor"
type: agent
agent: pesquisador
execution: inline
depends_on: step-01
outputFile: output/contexto.md
---

# Step 02 — Pesquisador: Pesquisar Contexto e Setor

## Para o Pipeline Runner

O Pesquisador busca dados externos para enriquecer o diagnóstico com benchmarks
do setor, análise de concorrentes e tendências do mercado do prospect.

## O que pesquisar

### 1. Benchmarks do setor
- Taxa de conversão média para o segmento
- Ticket médio típico no mercado
- Canais de aquisição mais usados por empresas similares
- Crescimento médio anual do setor

### 2. Análise de concorrentes (se identificados no briefing)
- Presença digital: canais ativos, frequência, qualidade
- Posicionamento de preço
- Pontos fracos visíveis (avaliações, reclamações públicas)
- Diferenciais que comunicam
- Skill: `33-marketing-concorrentes`

### 3. Tendências e oportunidades do segmento
- Novos canais de aquisição emergindo no setor
- Mudanças de comportamento do consumidor do segmento
- Oportunidades sazonais relevantes

## Regras

- Usar apenas dados verificáveis — indicar fonte quando possível
- Se não houver dados públicos suficientes: registrar "sem dados disponíveis" e prosseguir
- Focar no que é acionável para o diagnóstico — não criar relatório genérico de mercado
- Priorizar o `segmento` e a `região` do prospect (se identificada)

## Output esperado

Salvar em `output/contexto.md`:

```markdown
# Contexto de Mercado — [Empresa] — [Segmento]

## Benchmarks do Setor
| Métrica | Benchmark de mercado | Situação do prospect |
|---------|---------------------|---------------------|
| Taxa de conversão | X% | X% (briefing) |
| Ticket médio | R$ X | R$ X (briefing) |
| CAC médio | R$ X | — |

## Análise de Concorrentes
| Concorrente | Canais | Ponto fraco | Diferencial |
|-------------|--------|-------------|-------------|
| [nome] | [canais] | [fraqueza] | [diferencial] |

## Tendências e Oportunidades
- [tendência]: [relevância para o prospect]

## Gaps identificados (vs. concorrência e benchmarks)
- [gap]: [impacto no negócio do prospect]
```
