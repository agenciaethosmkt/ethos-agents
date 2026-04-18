---
step: "08"
name: "Entregar no ClickUp"
type: agent
agent: maya
execution: inline
depends_on: step-07
outputFile: output/entrega.md
---

# Step 08 — Maya: Entrega no ClickUp

## Para o Pipeline Runner

Maya registra tudo no ClickUp, envia os próximos passos ao cliente e
notifica as áreas internas com a passagem interna.

## Processo

### 1. Criar documento de onboarding no ClickUp

```
clickup_create_document(
  name="Onboarding — {cliente_nome}",
  parent_id=task.space.id,
  content=passagem_interna + notas_reuniao
)
```

### 2. Postar passagem interna como comentário na task

```
clickup_create_task_comment(task_id,
  "✅ Onboarding concluído — {cliente_nome} ({plano})\n\n
  {passagem_interna resumida}\n\n
  📎 Documento completo: [link]\n\n
  📋 Próximos passos enviados ao cliente via WhatsApp.",
  notify_all=true
)
```

### 3. Enviar próximos passos ao cliente via WhatsApp

Seguir protocolo Maya — mostrar mensagem exata para aprovação antes de enviar:

```
Mensagem para {responsavel_cliente} ({whatsapp_cliente}):
---
{conteúdo de output/proximos-passos.md adaptado para WhatsApp}
---
Confirma envio? (manda / ajusta / cancela)
```

Após aprovação:
```bash
python3 ~/.claude/skills/whatsapp/scripts/whatsapp.py send {whatsapp_cliente} "{texto}"
```

### 4. Atualizar task no ClickUp

```
clickup_update_task(task_id, status="em revisão")
clickup_update_task(task_id, remove_assignees=[101151431])
clickup_update_task(task_id, add_assignees=[task.creator.id])
```

### 5. Registrar no log de execuções

```
clickup_create_task(
  list_name="Agente: Log de Execuções",
  name="Onboarding — {cliente_nome} — {plano}",
  description="task_id: {task_id}\nsquad: onboarding-cliente\ncliente: {cliente_nome}\nplano: {plano}\nstatus: sucesso\ntimestamp: {ISO datetime}"
)
```

### 6. Atualizar memória da Maya

Registrar em `~/.claude/skills/whatsapp/memory/contacts/{whatsapp_cliente}.md`:
- Nome, cargo, empresa
- Canal de comunicação preferido
- Tom e estilo observado
- Próxima data de contato combinada
