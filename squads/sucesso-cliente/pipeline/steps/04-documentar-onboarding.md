# Step 04 — Documentar Onboarding

**Persona:** Redator  
**Objetivo:** Criar documento de resumo do onboarding no ClickUp com base nas anotações da reunião.

## Inputs

- Anotações do CS (comentário da task após a reunião)
- `cliente_nome`, `plano_contratado`, `responsavel_cs`, `responsavel_cliente`

## Execução

Ler o comentário com as anotações da reunião e gerar documento estruturado:

```
## Resumo de Onboarding — [cliente_nome] — [data]

**Plano contratado:** [plano_contratado]
**CS responsável:** [responsavel_cs]
**Responsável do cliente:** [responsavel_cliente + contato]
**Canal de comunicação oficial:** [WhatsApp / Email]

### Contexto do negócio
[descrição do negócio, segmento, diferenciais]

### Objetivos principais do cliente
1.
2.
3.

### Prioridades iniciais
[o que é mais urgente resolver]

### Ofertas/serviços prioritários
[produtos/serviços a focar primeiro]

### Restrições, urgências e pontos sensíveis
[o que não pode errar, prazos críticos, histórico negativo]

### Responsáveis por aprovações e envios
| Responsabilidade | Contato |
|---|---|
| Aprovação de conteúdo | |
| Envio de materiais | |
| Decisão de investimento | |

### Riscos identificados
[sinais de atenção percebidos durante a reunião]
```

## Output

```
clickup_create_document(
  name="Onboarding — {cliente_nome}",
  parent_id=task.space.id,
  content=[documento acima]
)
```

Salvar `doc_url` para usar no Step 05 e 06.
