---
step: "04"
name: "Revisar Roteiro"
type: agent
agent: revisor
execution: inline
depends_on: step-03
outputFile: output/revisao.md
---

# Step 04 — Revisor: Revisar Roteiro

## Para o Pipeline Runner

O Revisor analisa o roteiro contra os critérios em `pipeline/data/quality-criteria.md`
e os anti-padrões em `pipeline/data/anti-patterns.md`.

## Checklist de revisão

### Estrutura
- [ ] Gancho está nos primeiros 3 segundos
- [ ] Cena 1 não começa com apresentação ou "olá"
- [ ] Número de cenas bate com a estrutura do step-02
- [ ] Duração estimada dentro do `duracao_alvo` (± 5s)
- [ ] Última cena tem CTA claro e específico

### Conteúdo por cena
- [ ] Cada cena tem exatamente: VISUAL + VOZ OFF + TEXTO NA TELA
- [ ] Uma ideia por cena (sem cenas sobrecarregadas)
- [ ] Frases de voz off com máximo 12 palavras
- [ ] Texto na tela complementa (não repete) a voz off
- [ ] Ritmo crescente — cada cena agrega valor

### Legenda e hashtags
- [ ] Legenda presente e dentro de 150 chars
- [ ] Gancho da legenda diferente do gancho visual
- [ ] 3–5 hashtags presentes

### Notas de produção
- [ ] Notas de produção presentes e acionáveis para o editor

## Decisão

### Se APROVADO
Prosseguir para step-05.

### Se REPROVADO
Listar itens com falha e devolver ao Ogilvy para correção pontual.
Máximo 2 ciclos. No 3º ciclo:

```
clickup_create_task_comment(task_id,
  "⚠️ Roteiro não passou na revisão após 2 ciclos. Revisar manualmente.\n\n[itens reprovados]")
clickup_update_task(task_id, status="em alteração & ajustes")
```
→ ABORTAR

## Output esperado

Salvar em `output/revisao.md`:

```markdown
# Revisão — Roteiro [Cliente] — [Tema]

**Resultado:** APROVADO | REPROVADO

## Checklist
[✅ / ❌ por item]

## Itens a corrigir (se REPROVADO)
- [item]: [problema] → [correção esperada]
```
