---
step: "04"
name: "Revisão de Copy"
type: agent
agent: revisor
execution: inline
condition: "fase == copy"
inputFile: output/copy.md
---

# Step 04 — Revisor: Gate de Qualidade da Copy

## Para o Pipeline Runner

O Revisor faz a checklist de qualidade antes de a copy ir para "Em Revisão" com Renato.
Se identificar problema, devolve ao Ogilvy antes de avançar. Máximo 2 tentativas.

## Checklist

- [ ] Copy alinhada com o objetivo declarado no briefing
- [ ] Gancho na primeira linha (feed, reels, stories)
- [ ] CTA presente e claro
- [ ] Tom adequado ao cliente (não genérico)
- [ ] Tamanho dentro dos limites do formato
- [ ] Hashtags presentes (se feed/carrossel/reels)
- [ ] Roteiro tem marcação de tempo/gancho (se reels)
- [ ] Notas de produção presentes (se reels/stories)

## Se reprovar

Devolver ao Ogilvy com feedback específico:
```
⚠️ Revisor: copy precisa de ajuste antes de ir para Renato.
Problema: [descrição específica]
Ação: [o que corrigir]
```

## Se aprovar

Avançar para step-05 (entrega).
