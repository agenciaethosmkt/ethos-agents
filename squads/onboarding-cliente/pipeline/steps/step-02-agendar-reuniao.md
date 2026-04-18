---
step: "02"
name: "Agendar Reunião"
type: agent
agent: maya
execution: inline
depends_on: step-01
inputFile: output/validacao.yaml
outputFile: output/mensagem-agendamento.md
---

# Step 02 — Maya: Redigir Mensagem de Agendamento

## Para o Pipeline Runner

Maya redige a mensagem de agendamento da reunião de onboarding para envio via WhatsApp.
A mensagem será revisada por um humano antes do envio (checkpoint no step-03).

**Se persona = eletricistas:** redigir mensagem informando que o formulário de briefing foi enviado (sem agendar reunião).

## Inputs

- `output/validacao.yaml` — dados validados do cliente
- `pipeline/data/mensagens-padrao.md` — templates de mensagem por plano

## Processo

1. Ler o template de mensagem correspondente ao plano do cliente
2. Personalizar com: nome do cliente, nome do CS responsável, plano contratado
3. Redigir 2 opções de horário para propor ao cliente (verificar agenda do CS se disponível)
4. Seguir protocolo de aprovação da Maya — nunca enviar sem confirmação humana

## Output esperado

Salvar em `output/mensagem-agendamento.md`:

```markdown
# Mensagem de Agendamento — [Cliente]

**Destinatário:** [nome] — [whatsapp]
**Remetente:** [CS responsável]
**Plano:** [plano]
**Persona:** [padrao / eletricistas]

---

## Mensagem proposta

[texto exato da mensagem para WhatsApp]

---

## Horários sugeridos para propor
- Opção 1: [data e hora]
- Opção 2: [data e hora]

## Notas para o CS
[contexto relevante sobre o cliente para a reunião]
```

## Veto Conditions

- Mensagem genérica sem nome do cliente → rejeitar
- Mensagem sem proposta de horário → rejeitar (exceto persona eletricistas)
- Tom robótico ou formal demais → rejeitar
