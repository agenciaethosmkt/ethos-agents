# Step 03 — Preparar a Reunião (Checkpoint Humano)

**Persona:** Atendimento  
**Objetivo:** Gerar checklist de preparação e estrutura da pauta para o CS usar na reunião.

## ⏸ CHECKPOINT

Este step tem checkpoint humano: a reunião é realizada pelo CS com o cliente.  
O agente prepara o material — o CS executa a reunião e registra as anotações.

## Inputs

- `cliente_nome`
- `plano_contratado`
- `areas_envolvidas`

## Execução

Gerar e postar na task:

```
## Preparação para Reunião de Onboarding — [cliente_nome]

### Revisar antes da call
[ ] Proposta comercial aprovada e escopo vendido
[ ] Informações coletadas pelo comercial
[ ] Dúvidas pendentes sobre o cliente

### Pauta da reunião (45-60min)
1. Abertura e boas-vindas
2. Apresentação dos envolvidos
3. Relembrar escopo contratado ([plano_contratado])
4. Explicar rotina de comunicação (canal oficial, frequência, responsáveis)
5. Alinhar expectativa de prazo e maturação dos resultados
6. Entender cenário atual do cliente
7. Validar prioridades iniciais
8. Explicar próximas etapas: briefing → acessos → setup
9. Tirar dúvidas
10. Encerrar com direcionamento objetivo

### O que registrar durante a call
- Contexto atual do negócio
- Principais objetivos do cliente
- Prioridades iniciais (o que é mais urgente)
- Ofertas/serviços prioritários
- Restrições, urgências e pontos sensíveis
- Responsáveis por aprovações e envios
```

## Retorno do checkpoint

Após a reunião, o CS deve:
1. Adicionar anotações da call como comentário na task
2. Re-atribuir a task ao Claude (ID: 101151431)
3. Manter a tag `para-agente`
4. Definir nova data de vencimento

O agente retoma no Step 04.
