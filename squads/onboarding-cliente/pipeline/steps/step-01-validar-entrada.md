---
step: "01"
name: "Validar Entrada"
type: agent
agent: maya
execution: inline
outputFile: output/validacao.yaml
---

# Step 01 — Maya: Validar Entrada do Cliente

## Para o Pipeline Runner

Maya valida se o cliente está pronto para iniciar o onboarding e identifica a persona.
Se algum campo obrigatório estiver ausente, abortar e solicitar preenchimento.

## Campos obrigatórios (buscar em task.custom_fields e task.description)

| Campo | Onde buscar |
|---|---|
| `cliente_nome` | Custom field "Cliente" ou nome da task |
| `plano` | Custom field "Plano" ou folder (Flow / Growth / Business / Connect) |
| `pagamento_confirmado` | Custom field "Pagamento" ou descrição |
| `contrato_assinado` | Custom field "Contrato" ou descrição |
| `responsavel_cliente` | Custom field "Responsável Cliente" ou descrição |
| `whatsapp_cliente` | Custom field "WhatsApp" ou descrição |
| `cs_responsavel` | Assignee humano da task (além de Claude) |

## Identificar a persona do cliente

```
if "eletric" in cliente_nome.lower() or plano == "Eletricistas":
    persona = "eletricistas"
    # Fluxo alternativo: sem reunião, apenas formulário
else:
    persona = "padrao"
    # Fluxo padrão: com reunião de onboarding
```

## Output esperado

Salvar em `output/validacao.yaml`:

```yaml
cliente_nome: ""
plano: ""              # Flow / Growth / Business / Connect / Eletricistas
persona: ""            # padrao / eletricistas
pagamento_confirmado: true/false
contrato_assinado: true/false
responsavel_cliente: ""
whatsapp_cliente: ""   # formato: 5511999999999
cs_responsavel: ""     # nome do CS interno responsável
task_id: ""
fluxo: ""              # padrao / eletricistas
```

## Se pagamento ou contrato não confirmados

```
clickup_update_task(task_id, status="em alteração & ajustes")
clickup_create_task_comment(task_id,
  "⚠️ Onboarding não iniciado.\n\n▸ Pagamento confirmado: [sim/não]\n▸ Contrato assinado: [sim/não]\n\nAtualize os campos e reenvie para o agente.")
```
→ ABORTAR pipeline

## Se persona = eletricistas

Postar comentário informando o fluxo diferenciado:
```
clickup_create_task_comment(task_id,
  "📋 Persona identificada: Eletricistas.\nFluxo: sem reunião de onboarding — formulário de briefing será encaminhado via automação Make.\nVerifique se a automação [Onboarding][Envio de Formulário de Briefing] foi acionada.")
```
→ Seguir pipeline normalmente (steps 02-03 adaptados para este fluxo)
