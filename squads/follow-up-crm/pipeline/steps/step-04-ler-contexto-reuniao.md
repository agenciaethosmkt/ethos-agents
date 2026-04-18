---
step: "04"
name: "Ler Contexto da Reunião"
type: agent
agent: analista-comercial
condition: "fase == followup"
---

# Step 04 — Ler Contexto da Reunião para o Follow-up

## Objetivo

Extrair tudo que é necessário para o Redator criar um follow-up personalizado — especialmente a transcrição da reunião via Tactiq no Google Drive.

## 1. Extrair dados básicos da task

```
clickup_get_task(task_id) → extrair:
- lead_nome          → nome do lead
- lead_empresa       → empresa/ramo de atividade
- lead_segmento      → clínica | eletricista | outro
- produto_sugerido   → Flow | Growth | outro
- dor_principal      → problema central (formulário ou qualificação)
- objecoes           → objeções registradas na task (se houver)
```

## 2. Buscar transcrição da reunião no Google Drive (Tactiq)

O Tactiq salva as transcrições automaticamente no Google Drive após cada reunião via Google Meet.

```
mcp__claude_ai_Google_Drive__search_files(
  query="tactiq {lead_nome}",
  mime_type="application/vnd.google-apps.document"
)
```

Se não encontrar pelo nome do lead, tentar pelo nome da empresa:
```
mcp__claude_ai_Google_Drive__search_files(
  query="tactiq {lead_empresa}"
)
```

Se encontrar → ler o conteúdo:
```
mcp__claude_ai_Google_Drive__read_file_content(file_id)
```

### O que extrair da transcrição

- Dores mencionadas (em palavras do próprio lead)
- Objeções levantadas
- O que Renato prometeu ou combinou
- Nível de interesse demonstrado (empolgado, hesitante, pediu para pensar)
- Concorrentes ou alternativas mencionadas
- Prazo que o lead mencionou para decidir

## 3. Fallback — buscar notas nos comentários da task

Se a transcrição não for encontrada no Drive, buscar comentários na task:
```
clickup_get_task_comments(task_id)
→ filtrar comentários de Renato (task.creator.id) com palavras-chave:
  "reunião", "conversa", "call", "combinamos", "próximo passo", "objeção"
```

## 4. Montar sumário de contexto para o Redator

```markdown
# Contexto para Follow-up — [Lead] — [Data]

## Dados do lead
- Nome: [nome]
- Empresa/Segmento: [empresa] — [segmento]
- Produto sugerido: [Flow/Growth/outro]
- Dor principal: [dor identificada na qualificação]

## Da transcrição da reunião (Tactiq)
- Fonte: [link do Drive ou "não encontrada"]
- Dores em palavras do lead: [citações diretas]
- Objeções levantadas: [lista]
- Combinado ao final: [próximo passo]
- Nível de interesse: [empolgado / hesitante / pediu para pensar]
- Prazo mencionado: [quando pretende decidir]
- Outros pontos relevantes: [concorrentes, dúvidas, etc.]

## Status do contexto
[ ] Transcrição Tactiq encontrada e lida
[ ] Apenas notas da task (sem transcrição)
[ ] Sem contexto de reunião — follow-up genérico por segmento
```

Passar esse contexto completo para o step-05 (Redator).
