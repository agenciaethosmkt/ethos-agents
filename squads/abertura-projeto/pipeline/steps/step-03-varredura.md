# Step 03 — Varredura dos Marcos

## Agente
analista-setup

## Objetivo
Verificar o status de todas as tasks vinculadas aos marcos do projeto.

## Inputs
- `projeto_id` — tarefa principal já carregada no step-02

## Ações

Da tarefa principal, os campos `list_relationship` de cada marco contêm as tasks vinculadas.
Iterar sobre cada marco e classificar cada task:

### Classificação de status

| Status ClickUp | Classificação |
|---|---|
| `finalizado` / `completa` / `finalizada` | ✅ Concluída |
| `execução` / `em andamento` | 🔄 Em andamento |
| `backlog` / `não iniciada` | ⏳ Não iniciada |
| due_date < hoje E não finalizada | 🔴 Atrasada |
| `revisão` / `em revisão` | 👁️ Aguardando revisão |

### Para cada marco disponível no produto, ler as tasks:

**Connect:**
- `[Connect] [1] Kickoff` → Onboarding, Diagnóstico do Perfil, Plan. Estratégico, Identidade Visual, Linha Editorial
- `[Connect] [2] Ativação e Testes` → Planejamento de Conteúdo Mensal, Impulsionamento de Conteúdos
- `[Connect] [3] Monitoramento e Otimização` → Relatórios, Monitoramento de Resultado dos Posts

**Flow:**
- `[Flow] [1] Kickoff` → tasks de kickoff Flow
- `[Flow] [2] Ativação & Testes` → tasks de ativação Flow
- `[Flow] [3] Validação & Escala` → tasks de validação Flow

**Growth:** todos os marcos Connect + Flow

## Calcular progresso por marco

```
total_tasks = len(tasks_do_marco)
concluidas = len([t for t in tasks if t.status == "concluída"])
progresso = (concluidas / total_tasks) * 100
```

## Identificar alertas

- Task com due_date vencido e status não finalizado → ATRASO
- Marco com 0% progresso e due_date passado → MARCO BLOQUEADO
- Task sem assignee → SEM RESPONSÁVEL

## Output
```
varredura:
  marco_1:
    nome: "[nome]"
    progresso: "X%"
    tasks: [{nome, status, classificacao, due_date, assignee}]
    alertas: [lista de alertas]
  marco_2:
    ...
  marco_3:
    ...
  resumo:
    total_tasks: N
    concluidas: N
    em_andamento: N
    atrasadas: N
    nao_iniciadas: N
```
