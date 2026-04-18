---
step: "07"
name: "Consolidar Briefing do Cliente"
type: agent
agent: analista-comercial
condition: "fase == fechamento"
outputFile: output/briefing-cliente.md
---

# Step 07 — Consolidar Briefing do Novo Cliente

## Objetivo

O negócio foi fechado. Consolidar um briefing completo do cliente para:
1. Alimentar o CRM (Gestão de Clientes) com dados precisos
2. Preparar o onboarding (squad `onboarding-cliente`)
3. Informar Sobral, Kizo e demais agentes que atuarão com este cliente

## Fontes de dados

```
clickup_get_task(task_id) → campos da task do lead
clickup_get_task_comments(task_id) → histórico da negociação
mcp__claude_ai_Google_Drive__search_files(query="tactiq {lead_nome}") → transcrição(ões) da(s) reunião(ões)
```

## Campos a consolidar

```markdown
# Briefing do Novo Cliente — [Nome] — [Data de Fechamento]

## Dados do negócio
- Nome: [nome completo]
- Empresa: [nome da empresa]
- Segmento: [clínica / eletricista / outro]
- Faturamento declarado: R$ [valor]/mês
- Cidade/Estado: [localização]
- WhatsApp: [número]
- E-mail: [e-mail]

## Contrato
- Plano contratado: [Flow / Growth / outro]
- Valor mensal: R$ [valor]
- Duração: [X meses]
- Data de início prevista: [data]
- Canal comercial de origem: [Meta LeadAds / indicação / outro]

## Contexto do negócio
- Dor principal: [o que motivou a contratação]
- Objetivo principal: [resultado esperado ao final do contrato]
- Produto/Serviço principal do cliente: [o que ele vende]
- Público-alvo do cliente: [para quem ele vende]
- Presença digital atual: [Instagram / site / Google Meu Negócio — state atual]

## Histórico da negociação
- Data do primeiro contato: [data]
- Data da reunião: [data]
- Objeções superadas: [lista]
- Condições especiais acordadas: [descontos, bônus, entregas extras — se houver]

## Notas para onboarding
[informações relevantes para a reunião de onboarding: expectativas específicas, alertas, pontos de atenção]
```

## Buscar dados faltantes

Se algum campo crítico estiver ausente, buscar nos comentários ou transcrições antes de registrar como "não informado".

Campos críticos: nome, WhatsApp, plano, valor, data de início.
