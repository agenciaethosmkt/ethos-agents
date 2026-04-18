---
step: "04"
name: "Preparar Reunião"
type: agent
agent: maya
execution: inline
depends_on: step-03
inputFile: output/validacao.yaml
outputFile: output/briefing-reuniao.md
---

# Step 04 — Maya: Preparar Briefing da Reunião

## Para o Pipeline Runner

Maya compila as informações disponíveis sobre o cliente para preparar o CS para a reunião de onboarding.
Buscar dados no ClickUp (task, CRM, proposta comercial) e montar o briefing.

**Se persona = eletricistas:** pular este step — não há reunião. Avançar diretamente para step-05.

## Inputs

- `output/validacao.yaml` — dados validados
- Task do cliente no ClickUp (campos custom + descrição + tasks linkadas)
- CRM: buscar registro do cliente em Comercial > CRM > Gestão de Clientes

## Processo

1. Ler campos custom da task: plano, produto, responsável comercial
2. Buscar task de proposta comercial linkada (se existir)
3. Buscar registro do cliente no CRM
4. Compilar briefing para o CS

## Output esperado

Salvar em `output/briefing-reuniao.md`:

```markdown
# Briefing de Reunião — [Cliente] — [Data]

## Dados do cliente
- **Empresa:** [nome]
- **Responsável:** [nome e cargo]
- **WhatsApp:** [número]
- **Plano contratado:** [plano]
- **Data de início:** [data]

## O que foi vendido
[resumo do escopo da proposta comercial]

## Contexto do negócio (do comercial)
[o que se sabe sobre o negócio do cliente]

## Dúvidas e pontos em aberto
[o que não ficou claro ou precisa ser confirmado na reunião]

## Pauta sugerida para a reunião
[baseada em pipeline/data/pauta-reuniao.md]

## Alertas e pontos de atenção
[riscos, urgências, expectativas específicas mencionadas no comercial]
```

## Veto Conditions

- Briefing sem escopo do que foi vendido → rejeitar (buscar na proposta linkada)
- Briefing sem pelo menos 3 pontos de atenção ou dúvidas → alertar CS
