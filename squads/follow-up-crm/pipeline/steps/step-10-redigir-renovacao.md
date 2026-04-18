---
step: "10"
name: "Redigir Abordagem de Renovação"
type: agent
agent: redator
condition: "fase == renovacao"
inputFile: output/analise-renovacao.md
outputFile: output/renovacao.md
---

# Step 10 — Redigir Abordagem de Renovação

## Objetivo

Criar uma mensagem de WhatsApp que abra a conversa de renovação de forma natural — não como cobrança, mas como continuidade de uma parceria.

## Regras de escrita

- **Tom:** parceiro que celebra o caminho percorrido juntos
- **Nunca:** "seu contrato vence em X dias" como abertura — parece cobrança
- **Sempre:** começar com algo real do relacionamento (resultado, conquista, contexto)
- **Comprimento:** 3–5 linhas — conversa inicial, não proposta completa

## Estrutura por cenário

### Relacionamento saudável com bons resultados

```
[celebrar conquista real do período]
[antecipar o que vem pela frente se continuar]
[abrir conversa sobre renovação de forma natural]
```

Exemplo:
> {nome}, foi um semestre bem diferente do que você tinha quando começamos — você saiu de [situação inicial] para [resultado alcançado].
>
> Tô pensando nas próximas etapas pra gente avançar e queria conversar sobre como continuar essa parceria. Quando você tem 15 minutinhos essa semana?

### Relacionamento com ressalvas (resultados abaixo ou insatisfação)

```
[reconhecer honestamente o período]
[mostrar aprendizado e o que mudaria]
[propor conversa franca antes de renovar]
```

Exemplo:
> {nome}, quero conversar com você antes do contrato vencer.
>
> Sei que alguns meses foram abaixo do esperado. Quero te mostrar o que mudou na estratégia e ouvir sua percepção antes de qualquer decisão.
>
> Quando posso te ligar?

### Possibilidade de upgrade

```
[destacar resultado que justifica o próximo passo]
[introduzir o upgrade como evolução natural, não venda]
[propor reunião para apresentar]
```

---

## Output — salvar em output/renovacao.md

```markdown
# Abordagem de Renovação — [Cliente] — [Data]

## Cenário identificado
[saudável com resultados / ressalvas / upgrade]

## Mensagem sugerida (WhatsApp)

---
[mensagem aqui]
---

## Variação alternativa

---
[variação aqui]
---

## Proposta de renovação (para a reunião)
- Plano atual: R$ [valor]/mês
- Proposta: [manter / upgrade para R$ valor / ajuste]
- Justificativa: [argumento baseado em resultado ou potencial]

## Notas para Renato
[alertas, pontos de atenção, o que mencionar ou evitar na conversa]
```
