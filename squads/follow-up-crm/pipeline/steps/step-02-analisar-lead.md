---
step: "02"
name: "Analisar Lead"
type: agent
agent: analista-comercial
condition: "fase == qualificacao"
outputFile: output/analise-lead.md
---

# Step 02 — Analisar Fit do Lead

## Objetivo

Determinar se o lead tem fit com a Ethos usando faturamento como critério principal (não orçamento declarado — faturamento reflete realidade do negócio).

## ICP da Ethos — Perfis de Cliente Ideal

### ICP 1 — Flow (Estruturação)
- **Perfil:** Clínica pequena ou negócio local liderado pelo próprio dono, com serviço validado mas sem aquisição previsível de clientes
- **Faturamento:** R$10.000 – R$20.000/mês
- **Dores:** agenda imprevisível, dependência de indicação, não sabe o que fazer em marketing
- **Produto indicado:** Flow

### ICP 2 — Growth (Expansão)
- **Perfil:** Negócio estruturado com equipe, marketing fragmentado, quer escalar com previsibilidade
- **Faturamento:** R$20.000 – R$50.000/mês
- **Dores:** engajamento sem conversão, leads sem processo, sem visão de CAC
- **Produto indicado:** Growth

### ICP 3 — Eletricistas e Serviços Técnicos
- **Perfil:** Autônomo ou pequena empresa de serviço técnico (elétrica, hidráulica, climatização, etc.) que depende de indicação e quer gerar demanda local
- **Faturamento:** R$8.000 – R$25.000/mês
- **Dores:** sem presença digital, sem fluxo de novos clientes, sem processo comercial
- **Produto indicado:** Flow ou pacote específico para serviços técnicos

### Aberto a novos públicos
A Ethos está em expansão. Outros segmentos podem ter fit se:
- Negócio local ou regional com serviço/produto validado
- Dono(a) como decisor(a)
- Faturamento mínimo de R$8.000/mês
- Aberto a investir em marketing como crescimento, não como custo

---

## Critérios de análise de fit

### ✅ Tem fit quando
- Faturamento ≥ R$8.000/mês
- É dono(a) ou sócio(a) — decide sozinho
- Tem negócio validado (já atende clientes)
- Quer crescer e entende que marketing é investimento
- Tem urgência real (quer começar em até 60 dias)

### ⚠️ Fit médio — aprofundar antes de avançar
- Faturamento entre R$5.000 e R$8.000/mês (analisar potencial e momento)
- Decisor presente mas precisa de aprovação de sócio
- Urgência baixa mas necessidade real
- Negócio novo (< 6 meses) com tração inicial

### ❌ Sem fit — desqualificar
- Faturamento abaixo de R$5.000/mês
- Quer parceria por resultado (comissão) sem contrato fixo
- Histórico de múltiplas trocas de agência com culpa terceirizada
- Quer "apenas mais seguidores" sem objetivo de negócio
- Não é o decisor e o decisor não está na conversa

---

## Fontes de dados

```
clickup_get_task(task_id) → extrair:
- Respostas do formulário LeadAds (na descrição ou campos custom)
- Comentários da qualificação via WhatsApp (se já houver)
- custom_fields["Faturamento"]
- custom_fields["Segmento"] ou "Ramo de Atividade"
- custom_fields["Plano de Interesse"]
- custom_fields["Canal de Origem"]
```

Se faturamento não declarado → estimar com base no segmento, tamanho da equipe e outros sinais disponíveis. Registrar como estimativa.

---

## Output — salvar em output/analise-lead.md

```markdown
# Análise de Fit — [Lead] — [Data]

## Dados do Lead
- Nome: [nome]
- Empresa/Segmento: [empresa] — [ramo]
- Canal de origem: [canal]
- Plano de interesse: [plano]
- Faturamento declarado/estimado: R$ [valor]/mês

## Análise de Fit

### Faturamento
[✅/⚠️/❌] R$ [valor]/mês — [dentro/abaixo/acima do perfil ICP]

### Perfil do decisor
[✅/⚠️/❌] [dono / sócio / funcionário — detalhar]

### Necessidade real
[✅/⚠️/❌] [qual dor foi identificada]

### Momento e urgência
[✅/⚠️/❌] [quer começar quando]

### ICP mais próximo
[ ] Flow  [ ] Growth  [ ] Eletricistas/Serviços Técnicos  [ ] Novo público

## Score de Fit
**[Alto / Médio / Baixo]** — [resumo em 1 linha]

## Recomendação
[ ] Avançar para reunião — produto sugerido: [produto]
[ ] Solicitar mais informações: [quais]
[ ] Desqualificar — motivo: [motivo claro e respeitoso]

## Próximos passos sugeridos para Renato
[ação específica com contexto]
```
