# Step 02 — Contexto do Projeto

## Agente
analista-setup

## Objetivo
Carregar o contexto completo do projeto a partir da tarefa principal (Painel de Projetos).

## Inputs
- `projeto_id` — ID da tarefa principal (vindo do step-01)

## Ações

```
clickup_get_task(projeto_id, subtasks=false, detail_level="detailed")
```

Extrair dos campos custom:
- `Cliente` (list_relationship) → nome do cliente
- `Produto` (dropdown) → Connect / Flow / Growth / Business
- `Valor` (currency) → mensalidade
- `start_date` → início do projeto
- `due_date` → prazo total do projeto
- Assignees: Estrategista, Designer, Social Media, Copywriter, Gestor de Tráfego
- `Contas a Receber` → quantas parcelas / status financeiro
- `Gestão Contratual` → status do contrato

## Buscar dados do cliente no CRM

```
clickup_get_task(cliente_task_id)
```

Do registro do cliente em Gestão de Clientes, extrair:
- Segmento / nicho do cliente
- Instagram / redes sociais (se disponível)
- Observações relevantes

## Veto Conditions

Se `projeto_id` não retornar tarefa válida → abortar com:
> "⚠️ Falconi: não consegui acessar a tarefa principal do projeto (ID: {projeto_id}). Verifique o relacionamento."

## Output
```
projeto:
  nome: "[nome da tarefa principal]"
  cliente: "[nome do cliente]"
  produto: "Connect | Flow | Growth"
  valor: "R$ X"
  start_date: "[data]"
  due_date: "[data]"
  assignees:
    estrategista: "[nome]"
    designer: "[nome]"
    social_media: "[nome]"
    copywriter: "[nome]"
  contrato_status: "em vigor | pendente"
  financeiro: "X parcelas — Y recebidas"
```
