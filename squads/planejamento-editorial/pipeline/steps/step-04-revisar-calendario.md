---
step: "04"
name: "Revisar Calendário"
type: agent
agent: revisor
execution: inline
depends_on: step-03
outputFile: output/revisao.md
---

# Step 04 — Revisor: Revisar Calendário

## Para o Pipeline Runner

O Revisor analisa o calendário gerado pelo Ogilvy (step-03) contra os critérios de qualidade
definidos em `pipeline/data/quality-criteria.md` e os anti-padrões em `pipeline/data/anti-patterns.md`.

## Checklist de revisão

### Cobertura e distribuição
- [ ] Todos os pilares aparecem ao menos 1× por semana
- [ ] Nenhum pilar "Conversão" aparece 2 dias seguidos
- [ ] Nenhum pilar "Autoridade" representa mais de 30% do total
- [ ] "Prova Social" aparece ao menos 1× por quinzena
- [ ] Nenhuma data bloqueada (restricoes do briefing) foi utilizada
- [ ] Nenhum dia tem 2 posts agendados

### Qualidade por post
- [ ] Cada post tem: data, formato, pilar, tema, gancho, objetivo, CTA
- [ ] Ganchos são específicos e provocadores — não genéricos
- [ ] CTAs são variados (não repete o mesmo CTA na semana)
- [ ] Temas não se repetem no mesmo mês

### Aderência ao cliente
- [ ] Formatos estão dentro do que o cliente produz (verificar memória)
- [ ] Volume total está dentro do briefado

## Decisão

### Se APROVADO
Prosseguir para step-05.

### Se REPROVADO (falhou ≥ 1 item do checklist)
Listar exatamente o que falhou e devolver ao Ogilvy para correção.
O Ogilvy corrige apenas os itens apontados e retorna ao Revisor.

Máximo 2 ciclos de revisão. Se ainda reprovado no 2º ciclo:
```
clickup_create_task_comment(task_id,
  "⚠️ Calendário não passou na revisão após 2 ciclos. Revisar manualmente.\n\n[detalhes dos itens reprovados]")
clickup_update_task(task_id, status="em alteração & ajustes")
```
→ ABORTAR

## Output esperado

Salvar em `output/revisao.md`:

```markdown
# Revisão — Calendário Editorial — [Cliente] — [Mês/Ano]

**Resultado:** APROVADO | REPROVADO

## Itens verificados
[checklist com ✅ / ❌ por item]

## Itens a corrigir (se REPROVADO)
- [item]: [descrição do problema e correção esperada]
```
