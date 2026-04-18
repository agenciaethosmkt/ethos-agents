---
step: "03"
name: "Gerar Pauta Editorial"
type: agent
agent: ogilvy
execution: inline
depends_on: step-02
outputFile: output/calendario.md
---

# Step 03 — Ogilvy: Gerar Pauta Editorial

## Para o Pipeline Runner

Ogilvy cria o calendário editorial completo do mês usando o briefing (step-01) e o contexto (step-02).
Skill principal: `17-instagram-calendario`.

## Regras de distribuição

### Volume e frequência
- Distribuir posts uniformemente nas semanas do mês
- Nunca agendar 2 posts no mesmo dia
- Respeitar `restricoes` do briefing (datas bloqueadas)
- Dar preferência a: terça, quarta, quinta e sexta para feed/carrossel
- Stories podem ser diários se o volume permitir

### Distribuição por pilar
- Cada pilar deve aparecer ao menos 1× por semana
- Pilar "Autoridade" → máximo 30% do total (não exagerar em conteúdo educativo)
- Pilar "Prova Social" (depoimentos, casos) → ao menos 1× por quinzena
- Pilar "Conversão" (CTA direto para venda) → ao menos 1× por semana, mas nunca 2 dias seguidos

### Distribuição por formato
- Carrossel: ideal para conteúdo educativo e listas
- Reels: ideal para tendências, bastidores, tutoriais rápidos
- Post de Feed: ideal para frases de impacto, lançamentos, provas sociais
- Stories: complementar ao feed (bastidores, enquetes, CTAs)
- Proporção sugerida (ajustar por cliente): 40% carrossel, 30% reels, 20% feed, 10% stories

### Por post, definir obrigatoriamente
1. `data` — dia do mês (DD/MM/AAAA)
2. `formato` — carrossel / reels / feed / stories
3. `pilar` — qual pilar de conteúdo
4. `tema` — o assunto central (ex: "Como escolher o melhor plano de marketing")
5. `gancho` — primeira frase / headline do conteúdo (slide 1 do carrossel)
6. `topicos` — **apenas para carrossel**: 5 tópicos dos slides 2–6 (slide 7 = CTA fixo)
7. `objetivo` — awareness / engajamento / conversão / relacionamento
8. `cta` — qual ação o post pede ao final
9. `referencias` — referência visual ou de copy (opcional)

### Regra de carrossel
Carrossel tem **sempre 7 slides**. A pauta deve entregar:
- Slide 1: gancho (headline)
- Slides 2–6: 5 tópicos específicos (um por slide)
- Slide 7: CTA (definido no campo `cta`)
Não criar carrossel sem definir os 5 tópicos internos.

## Skills a invocar

- `17-instagram-calendario` — estrutura e lógica do calendário
- `20-conteudo-pauta-seo` — se houver pilares de SEO/blog no mix

## Output esperado

Salvar em `output/calendario.md`:

```markdown
# Calendário Editorial — [Cliente] — [Mês/Ano]

**Total de posts:** X  
**Volume semanal:** X posts/semana  
**Pilares cobertos:** [lista]  

---

## Semana 1 (01/MM – 07/MM)

| Data | Formato | Pilar | Tema | Gancho | Tópicos (slides 2–6) | Objetivo | CTA |
|------|---------|-------|------|--------|----------------------|----------|-----|
| DD/MM | Carrossel | Autoridade | Como fazer X | "Você está errando em X" | 1. Erro 1 / 2. Erro 2 / 3. Erro 3 / 4. Erro 4 / 5. Solução | Engajamento | Salva esse post |
| DD/MM | Reels | Prova Social | Case do cliente Y | "Resultado real em 30 dias" | — | Conversão | Manda mensagem |

## Semana 2 (08/MM – 14/MM)
[...]

## Semana 3 (15/MM – 21/MM)
[...]

## Semana 4 (22/MM – 31/MM)
[...]

---

## Observações e Oportunidades Sazonais
- [data]: [oportunidade identificada no step-02]
```
