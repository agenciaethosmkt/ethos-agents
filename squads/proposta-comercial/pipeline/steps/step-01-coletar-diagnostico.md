---
step: "01"
name: "Coletar Diagnóstico do Lead"
type: agent
agent: analista-comercial
outputFile: output/diagnostico.md
---

# Step 01 — Coletar Diagnóstico Completo do Lead

## Objetivo

Reunir tudo que existe sobre o lead antes de escrever uma palavra da proposta. Proposta sem diagnóstico é template. Diagnóstico é o que diferencia.

## 1. Ler dados da task no ClickUp

```
clickup_get_task(task_id) → extrair:
- lead_nome
- lead_empresa
- lead_segmento           → clínica / eletricista / outro
- lead_faturamento        → faturamento declarado ou estimado
- lead_produto_sugerido   → Flow / Growth / personalizado
- lead_dor_principal      → do formulário ou qualificação
- lead_objetivos          → o que quer alcançar
- lead_canal_origem       → Meta LeadAds / indicação / etc.
```

## 2. Buscar transcrição da reunião no Google Drive (Tactiq)

```
mcp__claude_ai_Google_Drive__search_files(query="tactiq {lead_nome}")
→ se encontrar: mcp__claude_ai_Google_Drive__read_file_content(file_id)
```

Também tentar com nome da empresa:
```
mcp__claude_ai_Google_Drive__search_files(query="tactiq {lead_empresa}")
```

Da transcrição, extrair:
- **Dores em palavras do lead** — citações diretas (usar na proposta, soa familiar)
- **Objetivo principal** — o que ele quer alcançar nos próximos 3–6 meses
- **Situação atual** — o que já tentou, o que não funcionou
- **Objeções levantadas** — o que preocupa o lead
- **Nível de comprometimento** — empolgado, hesitante, comparando concorrentes

## 3. Buscar comentários da qualificação na task

```
clickup_get_task_comments(task_id)
→ filtrar: score de fit, produto sugerido, análise BANT do step-02 do squad follow-up-crm
```

## 4. Construir diagnóstico estruturado

```markdown
# Diagnóstico — [Lead] — [Data]

## Perfil
- Nome: [nome]
- Empresa: [empresa]
- Segmento: [segmento]
- Faturamento: R$ [valor]/mês
- ICP: [Flow / Growth / Eletricista / Personalizado]

## Situação atual (em palavras do lead)
"[citação direta da transcrição ou formulário]"

## Dores identificadas
1. [dor 1 — específica e concreta]
2. [dor 2]
3. [dor 3]

## Objetivo principal
[o que ele quer nos próximos 3–6 meses — específico]

## O que já tentou
[histórico de marketing anterior, se mencionado]

## Objeções a neutralizar na proposta
[lista]

## Tom recomendado para a proposta
[baseado no perfil: mais técnico / mais emocional / mais orientado a resultado]
```
