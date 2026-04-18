# Step 02 — Gerar Mensagem de Agendamento

**Persona:** Redator  
**Objetivo:** Gerar mensagem personalizada para o CS enviar ao cliente via WhatsApp agendando a reunião de onboarding.

## Inputs

- `cliente_nome` (responsável do cliente)
- `responsavel_cs` (nome do CS que vai enviar)
- `plano_contratado`

## Execução

Redigir mensagem no tom da Ethos — acolhedora, profissional, clara:

```
Olá, [cliente_nome]! 👋

Aqui é [responsavel_cs] da Ethos. Seu projeto foi confirmado e estamos muito felizes em ter você conosco! 🎉

O próximo passo é marcarmos nossa reunião de onboarding — uma call para alinhar tudo e garantir que o início seja impecável.

Tenho disponibilidade nos seguintes horários:
📅 [Opção 1]
📅 [Opção 2]
📅 [Opção 3]

Qual funciona melhor para você?
```

## Output

Postar como comentário na task:

```
clickup_create_task_comment(task_id,
  "📩 Mensagem de agendamento gerada — enviar via WhatsApp para [cliente_nome]:\n\n[mensagem]")
```

> Nota: o CS copia a mensagem e envia manualmente pelo WhatsApp do cliente. Registrar data de envio na task após envio.
