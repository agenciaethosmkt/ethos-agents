---
step: "03"
name: "Escrever Roteiro"
type: agent
agent: ogilvy
execution: inline
depends_on: step-02
outputFile: output/roteiro.md
---

# Step 03 — Ogilvy: Escrever Roteiro

## Para o Pipeline Runner

Com a estrutura definida no step-02, Ogilvy escreve o roteiro completo cena a cena.
Skills a invocar: `18-instagram-roteiro` e `22-conteudo-script-video`.

## Formato obrigatório por cena

Cada cena deve ter exatamente 3 elementos:

```
[CENA N] — [duração estimada em segundos]
VISUAL: [o que aparece na tela — descrição para o editor/produtor]
VOZ OFF: [o que é dito — ou "silêncio" se não houver]
TEXTO NA TELA: [legenda sobreposta — ou "nenhum" se não houver]
```

## Regras de escrita

### Gancho (cena 1)
- Máximo 3 segundos
- Texto na tela obrigatório (aparece antes da voz terminar)
- Visual impactante: close no rosto, resultado final, ou elemento de surpresa
- Sem introduções ("olá, hoje vou falar sobre...") — vai direto ao gancho

### Cenas intermediárias
- Uma ideia por cena — nunca duas
- Frases curtas: máximo 12 palavras por voz off de cena
- Texto na tela complementa a voz, não repete exatamente
- Ritmo crescente: cada cena entrega mais valor que a anterior

### CTA (última cena)
- Específico: dizer exatamente o que fazer ("manda 'quero' no direct", "salva esse vídeo", "segue para mais")
- Nunca: "curte e compartilha" como único CTA
- Pode ser duplo CTA: ação imediata + ação de médio prazo

### Legenda do post
- Escrever a legenda que acompanha o Reels após o roteiro
- Máximo 150 chars visíveis (antes de "mais")
- Gancho da legenda diferente do gancho visual
- Hashtags: 3–5, no comentário (não na legenda)

## Verificar consistência com estrutura

Conferir que:
- Número de cenas bate com o definido no step-02
- Gancho da cena 1 é o mesmo escolhido no step-02
- CTA final é o mesmo definido no step-02
- Duração total estimada está dentro do `duracao_alvo`

## Output esperado

Salvar em `output/roteiro.md`:

```markdown
# Roteiro — [Cliente] — [Tema]

**Duração estimada:** Xs  
**Formato:** Reels 9:16  
**Objetivo:** [objetivo]  
**Áudio:** [sugestão de música/trilha]

---

[CENA 1] — 3s
VISUAL: [descrição do visual]
VOZ OFF: [texto falado]
TEXTO NA TELA: [legenda sobreposta em destaque]

[CENA 2] — 5s
VISUAL: [...]
VOZ OFF: [...]
TEXTO NA TELA: [...]

[...demais cenas...]

[CENA N — CTA] — 4s
VISUAL: [...]
VOZ OFF: [...]
TEXTO NA TELA: [...]

---

## Legenda do Post
[texto da legenda — 150 chars visíveis]

## Hashtags (comentário)
[3–5 hashtags]

## Notas de Produção
- [instrução para o editor/produtor: cortes, efeitos, música, ritmo]
- [referência visual se houver]
```
