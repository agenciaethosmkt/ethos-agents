---
step: "07"
name: "Revisão de Design"
type: agent
agent: revisor
execution: inline
condition: "fase == design"
inputFile: output/design-url.md
---

# Step 07 — Revisor: Gate de Qualidade do Design

## Checklist

- [ ] Dimensões corretas para o formato
- [ ] Tamanho de arquivo ≤ 2MB
- [ ] Copy do Ogilvy aplicada corretamente
- [ ] Identidade visual do cliente respeitada (cores, fontes, logo)
- [ ] Texto legível (não abaixo de 20px)
- [ ] Para carrossel: slide 1 tem gancho visual forte
- [ ] Para stories: cada frame é autoexplicativo

## Se reprovar

Devolver ao Designer com feedback específico antes de avançar.

## Se aprovar

Avançar para step-08 (entrega do design).
