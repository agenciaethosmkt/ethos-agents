---
step: "07"
name: "Passagem Interna"
type: agent
agent: redator
execution: inline
depends_on: step-06
inputFile: output/notas-reuniao.md
outputFile: output/passagem-interna.md
---

# Step 07 — Redator: Documento de Passagem Interna

## Para o Pipeline Runner

O Redator monta o documento de passagem interna para alinhar todas as áreas da Ethos
sobre o novo cliente. Este documento vai como comentário na task do ClickUp.

## Inputs

- `output/notas-reuniao.md` — informações coletadas na reunião
- `output/validacao.yaml` — plano, persona e dados do cliente
- `output/proximos-passos.md` — o que foi combinado com o cliente

## Processo

Montar resumo objetivo para cada área envolvida: Tráfego Pago, Conteúdo/Design,
Financeiro/Jurídico (se aplicável) e time geral.

## Output esperado

Salvar em `output/passagem-interna.md`:

```markdown
# Passagem Interna — [Cliente] — [Plano] — [Data]

## Resumo executivo
[2-3 linhas: quem é o cliente, o que foi contratado, quando começa]

## Contexto do negócio
[o que a equipe precisa saber sobre o negócio do cliente]

## Prioridades iniciais
1. [prioridade 1]
2. [prioridade 2]
3. [prioridade 3]

## Restrições e pontos de atenção
⚠️ [restrição 1 — ex: "cliente teve experiência ruim com X, evitar"]
⚠️ [restrição 2]

## Para o Tráfego Pago
[o que Sobral precisa saber: produto prioritário, objetivo, orçamento disponível, histórico de campanhas]

## Para Conteúdo / Design
[o que Kizo/Ogilvy precisam saber: tom de voz, produto, público, restrições visuais]

## Para o CS (continuidade)
[o que Maya precisa registrar: canal de comunicação, frequência, aprovadores, próxima data de contato]

## Status de acessos e setup
[o que já foi solicitado, o que está pendente]

## Riscos identificados
🔴 [risco alto se houver]
🟡 [risco médio se houver]

## Próximo contato com o cliente
[data + canal + responsável]
```

## Veto Conditions

- Passagem sem seção de Tráfego Pago E Conteúdo → rejeitar (são as áreas críticas)
- Passagem sem riscos identificados (mesmo que seja "nenhum risco identificado") → rejeitar
- Passagem sem próxima data de contato → alertar
