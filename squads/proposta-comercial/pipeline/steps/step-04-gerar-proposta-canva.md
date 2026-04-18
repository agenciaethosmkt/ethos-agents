---
step: "04"
name: "Gerar Proposta no Canva"
type: agent
agent: designer
inputFile: output/conteudo-proposta.md
outputFile: output/proposta-canva.md
---

# Step 04 — Gerar Proposta Visual no Canva

## 1. Buscar brand kit da Ethos

```
mcp__claude_ai_Canva__list-brand-kits()
→ identificar brand kit "Ethos" ou "Ethos Marketing"
→ registrar brand_kit_id
```

## 2. Gerar proposta

```
mcp__claude_ai_Canva__generate-design(
  design_type="proposal",
  brand_kit_id="{brand_kit_id}",
  query="Proposta comercial profissional para agência de marketing digital.
    Cliente: {lead_nome} — {lead_empresa} — segmento: {segmento}.
    Plano: {plano} (Flow/Growth).
    Seções: capa personalizada com nome do cliente, diagnóstico do cliente,
    resultado esperado, método em 3 pilares, prova social com case,
    entregas incluídas, equipe, cronograma, investimento, CTA.
    Tom: profissional, moderno, direto. Cores da identidade Ethos.
    Conteúdo completo: {resumo do conteudo-proposta.md}",
  user_intent="Gerar proposta comercial personalizada para lead da Ethos Marketing"
)
```

## 3. Criar design a partir do candidato

Após geração, o Canva retorna candidatos. Selecionar o mais adequado:

```
mcp__claude_ai_Canva__create-design-from-candidate(
  candidate_id="{id_do_candidato_selecionado}",
  user_intent="Criar proposta comercial Ethos para {lead_nome}"
)
→ registrar design_id (começa com "D")
```

## 4. Verificar conteúdo gerado

```
mcp__claude_ai_Canva__get-design-content(design_id)
→ verificar se todas as seções estão presentes
→ verificar se nome do lead está na capa
```

## 5. Obter thumbnail para preview

```
mcp__claude_ai_Canva__get-design-thumbnail(design_id)
→ registrar URL do thumbnail para incluir no comentário ClickUp
```

## Output — salvar em output/proposta-canva.md

```markdown
# Proposta Canva — [Lead] — [Data]

## Design ID
[design_id — começa com "D"]

## Link de edição
https://www.canva.com/design/{design_id}/edit

## Thumbnail
[URL do thumbnail]

## Instrução para Renato
1. Abrir o link acima no Canva
2. Revisar e ajustar textos se necessário
3. Publicar como Website: Compartilhar → Publicar como site → Copiar link
4. Enviar o link canva.site/... para o lead via WhatsApp

## Observação
Solução interim até o template Next.js estar pronto.
```
