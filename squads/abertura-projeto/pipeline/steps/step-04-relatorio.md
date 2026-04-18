# Step 04 — Relatório de Acompanhamento

## Agente
redator

## Objetivo
Escrever o comentário de acompanhamento na tarefa principal do projeto.

## Inputs
- `projeto` — contexto do step-02
- `varredura` — status dos marcos do step-03
- `marco_ativado` — marco que disparou este ciclo

## Formato do comentário

Postar na tarefa principal (`projeto_id`) via:
```
clickup_create_task_comment(task_id=projeto_id, comment_text=relatorio, notify_all=true)
```

### Estrutura do relatório

```
📊 Acompanhamento de Projeto — {data_hoje}
Marco ativado: {marco_ativado.nome}

━━━━━━━━━━━━━━━━━━━━━━━━
📌 VISÃO GERAL
Cliente: {projeto.cliente}
Produto: {projeto.produto} | Valor: {projeto.valor}
Início: {start_date} | Prazo: {due_date}

━━━━━━━━━━━━━━━━━━━━━━━━
🗂️ STATUS DOS MARCOS

[Marco 1 — Kickoff] {progresso}%
{emoji} {task.nome} — {classificacao}
{emoji} {task.nome} — {classificacao}
...

[Marco 2 — Ativação] {progresso}%
...

[Marco 3 — Monitoramento] {progresso}%
...

━━━━━━━━━━━━━━━━━━━━━━━━
📈 RESUMO
✅ Concluídas: N | 🔄 Em andamento: N | ⏳ Não iniciadas: N | 🔴 Atrasadas: N

━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ ALERTAS
{lista de alertas — só mostrar se existirem}

━━━━━━━━━━━━━━━━━━━━━━━━
➡️ PRÓXIMOS PASSOS
{1-3 ações prioritárias baseadas nos alertas e no marco atual}
```

## Regras do relatório

- Só incluir seção ALERTAS se houver alertas reais
- Próximos passos devem ser acionáveis e específicos (não genéricos)
- Tom direto, sem floreios — é um relatório de gestão
- Datas sempre no formato DD/MM/AAAA

## Output
Comentário postado na tarefa principal. ID do comentário registrado para log.
