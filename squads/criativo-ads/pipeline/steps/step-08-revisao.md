---
step: "08"
name: "Revisão Final"
type: agent
agent: revisor
execution: inline
depends_on: step-07
outputFile: output/revisao-final.md
---

# Step 08 — Revisor: Checklist de Qualidade

## Para o Pipeline Runner

O Revisor faz a checklist final antes da entrega no ClickUp.

## Inputs

- `output/briefing.yaml` — o que foi pedido
- `output/angulo-selecionado.yaml` — ângulo aprovado
- `output/copy.md` — copy aprovado
- `output/design-canva-url.md` — design aprovado
- `pipeline/data/quality-criteria.md` — critérios de qualidade

## Processo

Verificar alinhamento entre briefing → ângulo → copy → design:
- O copy responde ao objetivo da campanha?
- O design aplica corretamente o copy do Ogilvy?
- As dimensões estão corretas para a plataforma?
- O CTA está claro na imagem?
- Há consistência de marca (logo, cores, tom)?

## Output esperado

Salvar em `output/revisao-final.md`:

```markdown
# Revisão Final — [Cliente] — [Produto]

## Status: APROVADO / APROVADO COM RESSALVAS / REPROVADO

## Checklist
- [x] Copy alinhado com o objetivo
- [x] Design aplica copy corretamente
- [x] Dimensões corretas ([plataforma]: [dimensões])
- [x] CTA visível e claro
- [x] Identidade de marca consistente
- [ ] [item com ressalva se houver]

## Ressalvas
[listar se houver]

## Recomendação para o próximo ciclo
[observação sobre o que testar na próxima rodada]
```

## Veto Conditions

- Status REPROVADO → não avançar para entrega, devolver para o agente responsável
- Dimensão incorreta detectada → devolver para Designer antes de entregar
