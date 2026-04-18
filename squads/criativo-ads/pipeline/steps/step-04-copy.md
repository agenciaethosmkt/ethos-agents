---
step: "04"
name: "Copy do Anúncio"
type: agent
agent: ogilvy
execution: inline
depends_on: step-03
inputFile: output/angulo-selecionado.yaml
outputFile: output/copy.md
---

# Step 04 — Ogilvy: Escrita do Copy

## Para o Pipeline Runner

O Ogilvy lê o ângulo aprovado e o briefing e escreve o copy completo do anúncio.
Seguir o protocolo TIPO 1 do `Ogilvy.md` (Copy de Anúncio).

## Inputs

- `output/angulo-selecionado.yaml` — ângulo aprovado com ajustes do humano
- `output/briefing.yaml` — cliente, público, plataforma, formato, tom
- `pipeline/data/quality-criteria.md` — critérios de qualidade

## Processo

1. Ler o ângulo selecionado e os ajustes do humano
2. Escrever copy adaptado ao formato e plataforma:
   - **Meta Ads** → skill `03-meta-copy-criativo`: headline + primary text + CTA
   - **Google Ads** → skill `07-google-copy`: RSA headlines + descriptions
3. Entregar 2 variações para A/B test

## Output esperado

Salvar em `output/copy.md`:

```markdown
# Copy — [Cliente] — [Produto] — [Ângulo]

**Plataforma:** [Meta / Google]
**Formato:** [imagem / vídeo / carrossel / RSA]
**Ângulo:** [nome do ângulo selecionado]

---

## VARIAÇÃO A

**Headline (até 40 chars Meta / 30 chars Google):**
[headline]

**Primary Text / Description:**
[copy completo — hook + desenvolvimento + CTA]

**CTA Button:** [Saiba Mais / Comprar / Cadastre-se]

---

## VARIAÇÃO B
[idem]

---

## Instruções de Design para o Kizo

- Elemento visual principal: [o que mostrar]
- Texto na imagem: [headline ou frase curta]
- Clima/mood: [ex: aspiracional, urgência, humano]
- Restrições: [o que NÃO mostrar]
```

## Veto Conditions

- Headline genérica sem especificidade → rejeitar
- Copy sem CTA → rejeitar
- Variações A e B idênticas → rejeitar
- Desalinhamento com o ângulo aprovado → rejeitar
