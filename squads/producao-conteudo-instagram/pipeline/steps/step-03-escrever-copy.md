---
step: "03"
name: "Escrever Copy"
type: agent
agent: ogilvy
execution: inline
condition: "fase == copy"
inputFile: output/briefing.yaml
outputFile: output/copy.md
---

# Step 03 — Ogilvy: Escrever Copy

## Para o Pipeline Runner

O Ogilvy escreve a copy completa com base no briefing e no formato detectado.
Injetar a skill correspondente ao formato (campo `skill` do briefing).

## Inputs

- `output/briefing.yaml` — briefing completo
- `pipeline/data/skills-por-formato.md` — guia de estrutura por formato
- `pipeline/data/quality-criteria.md` — critérios de qualidade

## Processo por formato

### Post de Feed / Carrossel → skill `16-instagram-copy`
- Escrever legenda completa: gancho + desenvolvimento + CTA + hashtags
- Para carrossel: escrever texto de cada slide (título + corpo, máx. 2 linhas por slide)

### Reels → skill `18-instagram-roteiro`
- Escrever roteiro completo: gancho (0-3s) + desenvolvimento + CTA final
- Incluir notas de produção (cenário, texto na tela, trilha sonora sugerida)

### Stories → skill `16-instagram-copy`
- Escrever sequência de stories: cada frame com texto curto e CTA
- Indicar stickers/elementos interativos (enquete, caixa de perguntas, link)

### E-mail → skill `31-marketing-email`
- Assunto (3 opções) + preview text + corpo completo com CTA

### WhatsApp → skill `24-whatsapp-disparos`
- Texto de disparo com personalização, links e CTA

## Output esperado

Salvar em `output/copy.md`:

```markdown
# Copy — [Cliente] — [Formato] — [Data de publicação]

**Formato:** [formato]
**Objetivo:** [objetivo]
**Pilar:** [pilar]

---

## Legenda / Roteiro / Script

[copy completa no formato correspondente]

---

## Hashtags (se feed/carrossel/reels)

[hashtags separadas em grupos: nicho / micro-nicho / marca]

---

## Notas de produção (se reels/stories)

[instruções para gravação ou design]
```

## Veto Conditions

- Copy sem gancho na primeira linha (feed/reels) → rejeitar
- Legenda sem CTA → rejeitar
- Roteiro sem indicação do gancho dos primeiros 3 segundos (reels) → rejeitar
- Copy com mais de 2200 caracteres sem quebras (limite Instagram) → alertar
