---
step: "06"
name: "Design Visual"
type: agent
agent: designer
execution: inline
depends_on: step-05
inputFile: output/copy.md
outputFile: output/design-canva-url.md
---

# Step 06 — Designer: Produção do Design no Canva

## Para o Pipeline Runner

O Designer produz o visual do anúncio no Canva com base no copy aprovado pelo Ogilvy.

## Inputs

- `output/copy.md` — copy aprovado + instruções de design do Ogilvy
- `output/briefing.yaml` — cliente, plataforma, formato
- `pipeline/data/formatos-ads.md` — dimensões técnicas por formato e plataforma

## Processo

### 1. Buscar template do cliente no Canva
```
canva_search_designs(query="{cliente} anúncio")
```
Se existir → usar como base. Se não → buscar na biblioteca:
```
canva_search_designs(query="{formato} ad template")
```

### 2. Criar design para cada variação aprovada
```
canva_create_design(
  design_type="{formato}",
  title="{cliente} — {produto} — Variação {A/B}"
)
```

### 3. Aplicar copy e identidade visual
- Inserir headline, texto e CTA conforme "Instruções de Design" do Ogilvy
- Aplicar brand kit do cliente (se disponível no Canva)
- Seguir dimensões exatas de `pipeline/data/formatos-ads.md`

### 4. Exportar
```
canva_export_design(design_id, format="png")
```

## Output esperado

Salvar em `output/design-canva-url.md`:

```markdown
# Design — [Cliente] — [Produto]

## Variação A
- **URL Canva:** [link]
- **Export:** [caminho do PNG]
- **Dimensões:** [ex: 1080×1080px]

## Variação B (se aprovada)
- **URL Canva:** [link]
- **Export:** [caminho do PNG]
- **Dimensões:** [ex: 1080×1080px]

## Notas de produção
[ajustes feitos em relação às instruções do Ogilvy]
```

## Fallback — Canva indisponível

Gerar briefing visual detalhado usando skill `46-design-prompts-ia`:
- Layout e hierarquia visual
- Paleta de cores com hex codes
- Tipografia (fonte, tamanho, peso)
- Prompt para geração via IA

## Veto Conditions

- Design sem copy do Ogilvy aplicado → rejeitar
- Dimensões incorretas para a plataforma → rejeitar
- Texto na imagem ilegível (< 20px) → rejeitar
- Mais de 20% da área coberta por texto (regra Meta) → alertar
