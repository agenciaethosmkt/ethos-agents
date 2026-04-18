---
step: "04"
name: "Revisar Diagnóstico"
type: agent
agent: revisor
execution: inline
depends_on: step-03
outputFile: output/revisao.md
---

# Step 04 — Revisor: Revisar Diagnóstico

## Para o Pipeline Runner

O Revisor analisa o diagnóstico contra os critérios em `pipeline/data/quality-criteria.md`
e os anti-padrões em `pipeline/data/anti-patterns.md`.

## Checklist de revisão

### Completude
- [ ] Todas as 7 seções do Raio X estão presentes
- [ ] Análise do funil cobre todas as 5 etapas (Atração → Pós-venda)
- [ ] Diagnóstico tem no mínimo 3 gargalos identificados
- [ ] Projeção de oportunidade presente com números

### Qualidade analítica
- [ ] Gargalos têm causa raiz identificada (não só sintoma)
- [ ] Cada gargalo tem impacto estimado em R$ ou %
- [ ] Benchmarks usados e comparados com a situação do prospect
- [ ] Recomendação Ethos conectada diretamente ao gargalo (não genérica)
- [ ] Máximo 3 serviços recomendados

### Acionabilidade
- [ ] Próximos passos claros e com prazo sugerido
- [ ] Linguagem objetiva — sem jargão desnecessário
- [ ] Diagnóstico pode ser apresentado em reunião sem adaptação

### Consistência
- [ ] Dados do diagnóstico batem com o briefing (step-01)
- [ ] Contexto de mercado (step-02) foi aproveitado no diagnóstico

## Decisão

### Se APROVADO
Prosseguir para step-05.

### Se REPROVADO
Listar itens com falha e devolver ao Analista Comercial para correção.
Máximo 2 ciclos. No 3º ciclo:

```
clickup_create_task_comment(task_id,
  "⚠️ Raio X não passou na revisão após 2 ciclos. Revisar manualmente.\n\n[itens reprovados]")
clickup_update_task(task_id, status="em alteração & ajustes")
```
→ ABORTAR

## Output esperado

Salvar em `output/revisao.md`:

```markdown
# Revisão — Raio X [Empresa]

**Resultado:** APROVADO | REPROVADO

## Checklist
[✅ / ❌ por item]

## Itens a corrigir (se REPROVADO)
- [item]: [problema] → [correção esperada]
```
