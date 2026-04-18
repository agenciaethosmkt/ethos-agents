---
step: "01"
name: "Detectar Fase"
type: agent
agent: ogilvy
execution: inline
---

# Step 01 — Detectar Fase Atual

## Para o Pipeline Runner

Identificar em qual etapa do processo a task se encontra com base no nome da lista.
Toda a execução posterior depende desta detecção.

## Lógica de detecção

```
lista = task.list.name

if lista == "Processo de Copywriting":
    fase = "copy"

elif lista == "Processo de Design & Criação":
    fase = "design"

elif lista == "Agendamentos, Publicações & Disparos":
    fase = "agendamento"

else:
    fase = "desconhecida"
    → comentar na task e abortar
```

## Se fase = "copy"
→ Executar steps 02, 03, 04, 05

## Se fase = "design"
→ Executar steps 06, 07, 08

## Se fase = "agendamento"
→ Executar step 09

## Se fase = "desconhecida"

```
clickup_create_task_comment(task_id,
  "⚠️ Lista não reconhecida pelo squad producao-conteudo-instagram.\nLista atual: {task.list.name}\nEscalando para revisão humana.")
```
→ ABORTAR
