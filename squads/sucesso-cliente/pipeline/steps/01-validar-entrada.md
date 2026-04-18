# Step 01 — Validar Entrada do Cliente

**Persona:** Atendimento  
**Objetivo:** Confirmar que todas as condições estão satisfeitas antes de iniciar o onboarding.

## Inputs necessários

Da task e campos custom:
- `cliente_nome` — nome da empresa e responsável principal
- `plano_contratado` — Flow / Growth / Business / Connect
- `pagamento_confirmado` — status do pagamento
- `contrato_validado` — status do contrato
- `responsavel_cs` — quem acompanha internamente

## Execução

1. Verificar `pagamento_confirmado` e `contrato_validado` nos campos da task
2. Identificar `plano_contratado` para saber quais áreas acionar
3. Identificar se cliente é da persona **Eletricistas** → se sim, registrar flag `skip_reuniao: true`

## Validações obrigatórias

| Campo | Se ausente |
|---|---|
| Pagamento confirmado | Comentar → solicitar validação do financeiro → abortar |
| Contrato validado | Comentar → solicitar validação do jurídico → abortar |
| Plano contratado | Comentar → solicitar preenchimento → abortar |
| Nome do responsável do cliente | Comentar → solicitar → abortar |

## Output

Contexto validado repassado para o Step 02:
```
cliente_nome: ...
plano_contratado: ...
responsavel_cliente: ...
responsavel_cs: ...
skip_reuniao: true/false
areas_envolvidas: [tráfego, conteúdo, design, ...]
```
