---
step: "02"
name: "Selecionar Case de Prova Social"
type: agent
agent: analista-comercial
inputFile: output/diagnostico.md
outputFile: output/case-selecionado.md
---

# Step 02 — Selecionar Case de Prova Social

## Objetivo

Encontrar um case de cliente Ethos do mesmo segmento que o lead para usar na proposta. Prova social de alguém parecido vale mais do que qualquer argumento.

## 1. Buscar cases no Google Drive

```
mcp__claude_ai_Google_Drive__search_files(
  query="case {segmento_do_lead}"
)
```

Tentativas de busca por segmento:
- Clínica Flow: `query="case clínica flow resultado"`
- Clínica Growth: `query="case clínica growth resultado"`
- Eletricistas: `query="case eletricista resultado"`
- Genérico: `query="case cliente ethos resultado"`

## 2. Buscar cases no ClickUp (Gestão de Clientes)

```
clickup_search(
  keywords="case resultado {segmento}",
  filters={list: "Gestão de Clientes"}
)
```

## 3. Critério de seleção

Priorizar case que tenha:
1. **Mesmo segmento** que o lead (clínica → clínica, eletricista → eletricista)
2. **Situação inicial parecida** (mesma dor ou contexto)
3. **Resultado mensurável** (números concretos: X leads/mês, X% crescimento)

Se não encontrar case do mesmo segmento → usar case com situação/dor parecida e adaptar.
Se não houver nenhum case → usar depoimento genérico de cliente satisfeito + indicar para Renato que este segmento ainda não tem case documentado.

## Output — salvar em output/case-selecionado.md

```markdown
# Case Selecionado para Proposta — [Lead]

## Case escolhido
- Cliente: [nome ou "Cliente X" se anônimo]
- Segmento: [segmento]
- Situação inicial: [contexto]
- Resultado alcançado: [resultado mensurável]
- Fonte: [link Drive ou "depoimento verbal"]

## Como usar na proposta
[trecho de 2–3 linhas pronto para inserir no slide de prova social]

## Alerta
[ ] Case do mesmo segmento encontrado
[ ] Case de segmento diferente (adaptar contexto)
[ ] Nenhum case — usar depoimento genérico
[ ] Renato: documentar este case após fechar (segmento sem case ainda)
```
