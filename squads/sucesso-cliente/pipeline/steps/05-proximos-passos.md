# Step 05 — Gerar Mensagem de Próximos Passos

**Persona:** Redator  
**Objetivo:** Gerar mensagem para o CS enviar ao cliente com os links de briefing, acessos e setup.

## Inputs

- `cliente_nome`
- `responsavel_cs`
- `plano_contratado`

## Links fixos dos processos

| Documento | Link |
|---|---|
| Briefing estratégico | `8cdvmy2-12857` |
| Solicitação de acessos | `8cdvmy2-12877` |
| Setup técnico | `8cdvmy2-12897` |

## Execução

Redigir mensagem com prazo claro (2 dias úteis a partir de hoje):

```
[cliente_nome], foi ótimo conversar! 🚀

Conforme combinamos, aqui estão os próximos passos:

1️⃣ *Briefing* — preencha o formulário para que a equipe já comece a trabalhar:
[link briefing]

2️⃣ *Acessos* — precisamos das permissões listadas aqui:
[link acessos]

3️⃣ *Setup técnico* — nossa equipe vai precisar de:
[link setup]

Prazo sugerido para envio: até [data — 2 dias úteis].

Qualquer dúvida, é só chamar aqui. Vamos juntos! 💪
[responsavel_cs] — Ethos
```

## Output

Postar como comentário na task:

```
clickup_create_task_comment(task_id,
  "📩 Mensagem de próximos passos — enviar via WhatsApp para [cliente_nome]:\n\n[mensagem]")
```
