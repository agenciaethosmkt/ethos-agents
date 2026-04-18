---
step: "06"
name: "Criar Design"
type: agent
agent: designer
execution: inline
condition: "fase == design"
outputFile: output/design-url.md
---

# Step 06 — Designer: Criar Design da Peça

## Para o Pipeline Runner

O Designer lê a copy aprovada (campo "Legenda" ou descrição da task) e cria a peça visual.

## Inputs a ler na task

```
clickup_get_task(task_id) → extrair:
- custom_fields["Legenda"]   → copy aprovada por Renato
- custom_fields["Formato"]   → formato da peça
- custom_fields["Cliente"]   → para buscar identidade visual
- custom_fields["Briefing"]  → contexto adicional
- task.description           → roteiro ou copy longa (Reels, e-mail)
```

## Processo por formato

### Post de Feed (1080×1080 ou 1080×1350)
- Criar no Canva com template do cliente
- Aplicar copy: headline na imagem + copy completa no campo "Legenda"
- Exportar PNG ≤ 2MB

### Carrossel (1080×1080 por slide)
- Criar slides via `instagram-carousel` (HTML→PNG) ou Canva
- Slide 1: capa com gancho visual forte
- Slides intermediários: um ponto por slide
- Slide final: CTA + perfil
- Exportar cada slide como PNG ≤ 2MB

### Stories (1080×1920)
- Criar no Canva — proporção 9:16
- Cada frame da sequência como arquivo separado
- Exportar PNG ≤ 2MB

### Reels
- Não há design automatizado para vídeo
- Gerar **briefing visual** detalhado com:
  - Texto na tela por cena
  - Sugestão de cenas/imagens
  - Referência de edição
- Postar briefing visual como comentário na task

## Regras de imagem

- Máximo **2 MB por arquivo** (limite ClickUp)
- Identidade visual do cliente tem prioridade sobre templates genéricos
- Buscar brand kit no Canva antes de criar do zero

## Output esperado

Salvar em `output/design-url.md`:

```markdown
# Design — [Cliente] — [Formato]

## Arquivos gerados
- [Arquivo 1]: [URL Canva ou caminho local] — [dimensões] — [tamanho]
- [Arquivo 2]: ...

## Notas de produção
[ajustes feitos, limitações encontradas]
```

## Veto Conditions

- Arquivo acima de 2MB → rejeitar (reduzir qualidade ou dimensões)
- Dimensões incorretas para o formato → rejeitar
- Design sem a copy do Ogilvy aplicada → rejeitar
