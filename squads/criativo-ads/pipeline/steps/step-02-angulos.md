---
step: "02"
name: "Ângulos Criativos"
type: agent
agent: estrategista
execution: inline
depends_on: step-01
inputFile: output/briefing.yaml
outputFile: output/angulos.md
---

# Step 02 — Estrategista: Geração de Ângulos Criativos

## Para o Pipeline Runner

O Estrategista Criativo lê o briefing e propõe 3 ângulos distintos para o criativo.
Cada ângulo é uma hipótese sobre o que vai mover o público a agir.

## Inputs

- `output/briefing.yaml` — briefing completo do criativo
- `pipeline/data/brief-format.md` — frameworks de ângulo disponíveis
- `pipeline/data/anti-patterns.md` — erros a evitar

## Processo

1. Analisar o objetivo, público e oferta do briefing
2. Identificar a dor principal, o desejo principal e a objeção principal do público
3. Propor 3 ângulos criativos distintos, cada um atacando um vetor diferente:
   - **Ângulo da Dor** — começa pelo problema que o público quer resolver
   - **Ângulo do Desejo** — começa pela transformação que o público quer alcançar
   - **Ângulo da Prova** — começa por resultado concreto, dado ou depoimento

## Output esperado

Salvar em `output/angulos.md`:

```markdown
# Ângulos Criativos — [Cliente] — [Produto]

**Briefing resumido:** [1 linha]
**Público:** [resumo]
**Objetivo:** [objetivo]
**Plataforma:** [plataforma]
**Formato:** [formato]

---

## Ângulo 1 — [Nome do ângulo]
**Vetor:** Dor / Desejo / Prova
**Hipótese:** [por que este ângulo vai funcionar com este público]
**Hook principal:** [primeira frase/imagem que abre o criativo]
**Desenvolvimento:** [como a narrativa evolui]
**CTA:** [ação esperada]
**Formato indicado:** [imagem / vídeo / carrossel]

## Ângulo 2 — [Nome do ângulo]
[idem]

## Ângulo 3 — [Nome do ângulo]
[idem]
```

## Veto Conditions

- Nenhum ângulo pode ser genérico ("Conheça nosso produto") — cada um precisa de hipótese específica
- Os 3 ângulos devem ser genuinamente distintos — não variações do mesmo tema
- O hook principal deve ser específico, não vago
