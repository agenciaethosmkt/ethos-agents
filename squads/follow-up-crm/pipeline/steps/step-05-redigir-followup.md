---
step: "05"
name: "Redigir Follow-up"
type: agent
agent: redator
condition: "fase == followup"
outputFile: output/followup.md
---

# Step 05 — Redigir Mensagem de Follow-up

## Objetivo

Criar uma mensagem de WhatsApp que retome a conversa com propósito, baseada no que foi discutido na reunião — não um "oi, tudo bem, e aí?".

## Regras de escrita

- **Tom:** próximo, direto, sem pressão — parceiro, não vendedor ansioso
- **Comprimento:** máximo 5 linhas no WhatsApp (mensagem que cabe na tela)
- **Personalização obrigatória:** usar algo específico da reunião (dor, frase do lead, contexto do negócio)
- **Nunca começar com:** "Oi, tudo bem?", "Olá!", "Passando para saber..."
- **Sempre ter:** referência ao que foi discutido + próximo passo claro

## Estrutura da mensagem por nível de interesse

### Lead empolgado (quer decidir logo)

```
[referência direta à dor ou objetivo do lead]
[o que a Ethos resolve — em 1 frase]
[próximo passo concreto: envio de proposta, link de contrato, etc.]
```

Exemplo:
> {nome}, pensando no que você falou sobre a dificuldade de agendar pacientes de forma consistente — isso é exatamente o que o nosso processo Flow resolve nos primeiros 30 dias.
>
> Posso te enviar a proposta hoje ainda pra você dar uma olhada?

### Lead hesitante (precisa de mais informação ou segurança)

```
[validar o que foi discutido — mostrar que ouviu]
[entregar algo de valor: case, dado, insight]
[próximo passo leve: pergunta aberta ou oferta de conversa rápida]
```

Exemplo:
> {nome}, saí da nossa conversa pensando na situação que você descreveu — negócio funcionando, mas dependendo demais de indicação.
>
> Separei um caso de uma clínica parecida que saiu desse padrão em 3 meses. Vale a pena te mandar?

### Lead pediu para pensar / sem prazo definido

```
[respeitar o espaço — sem pressão]
[entregar valor ou insight relevante]
[encerrar deixando porta aberta]
```

Exemplo:
> {nome}, sem pressa — é uma decisão importante.
>
> Enquanto isso, se surgir alguma dúvida sobre como funciona o processo ou quiser conversar mais, é só chamar.
>
> Fico à disposição.

## Mensagem para cada segmento (se sem transcrição)

### Clínicas (Flow/Growth)
Foco em: previsibilidade de agenda, fim da dependência de indicação, processo de aquisição de pacientes.

### Eletricistas e Serviços Técnicos
Foco em: gerar demanda local, aparecer no Google quando o cliente precisa, sair da dependência de indicação.

### Novos públicos
Foco em: problema mais citado na qualificação + resultado que a Ethos pode entregar.

---

## Output — salvar em output/followup.md

```markdown
# Follow-up — [Lead] — [Data]

## Contexto utilizado
- Fonte: [transcrição Tactiq / notas da task / genérico por segmento]
- Nível de interesse: [empolgado / hesitante / pediu para pensar]

## Mensagem sugerida (WhatsApp)

---
[mensagem aqui]
---

## Variação alternativa (se Renato quiser opção)

---
[variação aqui]
---

## Notas para Renato
[contexto da escolha do tom, referência usada, sugestão de horário de envio]
```
