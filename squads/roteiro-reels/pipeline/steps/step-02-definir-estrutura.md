---
step: "02"
name: "Definir Estrutura e Gancho"
type: agent
agent: ogilvy
execution: inline
depends_on: step-01
outputFile: output/estrutura.md
---

# Step 02 — Ogilvy: Definir Estrutura e Gancho

## Para o Pipeline Runner

Antes de escrever o roteiro completo, Ogilvy define a espinha dorsal do vídeo:
gancho, arco narrativo, número de cenas e CTA. Isso serve como blueprint para o step-03.

## Determinar duração e número de cenas

| Duração alvo | Cenas recomendadas | Ritmo |
|---|---|---|
| 15s | 3–4 cenas | Cortado rápido, sem voz off longa |
| 30s | 5–7 cenas | Médio, voz off + texto na tela |
| 45s | 8–10 cenas | Narrativo, pode ter storytelling |
| 60s | 10–14 cenas | Storytelling ou tutorial completo |

## Definir o gancho (primeiros 3 segundos)

O gancho é o único elemento que determina se o vídeo será assistido.
Deve ser decidido antes de qualquer cena ser escrita.

### Formatos de gancho que funcionam em Reels
- **Contradição:** "Tudo que te ensinaram sobre X está errado"
- **Promessa concreta:** "Em 30 segundos você vai aprender a fazer X"
- **Curiosidade:** "O motivo pelo qual X não funciona para você"
- **Identidade:** "Se você é [perfil], presta atenção nisso"
- **Número/lista:** "3 erros que estão sabotando seu X"
- **Resultado:** "Como meu cliente saiu de X para Y em 30 dias"

Se `gancho_sugerido` foi briefado: avaliar e adaptar ou usar se já for forte.
Se não foi briefado: criar 2 opções e escolher a melhor para o objetivo.

## Definir arco narrativo

Escolher um dos arcos abaixo conforme objetivo:

| Arco | Melhor para | Estrutura |
|---|---|---|
| **Problema → Solução** | Autoridade, Conversão | Dor → Por que acontece → Solução → CTA |
| **Lista** | Educação, Engajamento | Gancho → Item 1 → 2 → 3 → Conclusão → CTA |
| **Antes/Depois** | Prova Social, Conversão | Estado atual → Transformação → Resultado → CTA |
| **Tutorial** | Autoridade | Objetivo → Passo 1 → 2 → 3 → Resultado → CTA |
| **Storytelling** | Engajamento, Relacionamento | Contexto → Conflito → Virada → Lição → CTA |

## Output esperado

Salvar em `output/estrutura.md`:

```markdown
# Estrutura — Reels [Cliente] — [Tema]

**Duração alvo:** Xs  
**Número de cenas:** N  
**Arco narrativo:** [nome do arco]  
**Objetivo:** [awareness / engajamento / conversão / educação]

## Gancho (primeiros 3s)
[texto exato do gancho escolhido]
*Por que funciona: [razão em 1 linha]*

## Arco de cenas
1. [cena 1 — descrição em 1 linha]
2. [cena 2 — descrição em 1 linha]
...
N. [cena N — CTA]

## CTA final
[o que o vídeo pede ao espectador]

## Áudio/Música
[sugestão: trilha instrumental / trend / voz off / silêncio + legenda]
```
