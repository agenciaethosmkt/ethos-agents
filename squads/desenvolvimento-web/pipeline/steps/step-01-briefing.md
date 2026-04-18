# Step 01 — Ler Briefing e Identificar Tipo

## Agente
estrategista

## Objetivo
Ler a task completa, identificar o tipo de trabalho e carregar o contexto do cliente.

## Ações

```
clickup_get_task(task_id, detail_level="detailed")
```

Extrair:
- `task.name` — nome da task
- `task.description` — briefing completo
- `task.custom_fields` — campos custom (URL da página, cliente, produto, plataforma)
- `task.attachments` — referências visuais, wireframes, copies anexados
- `task.tags` — tags da task

## Identificação do tipo

| Palavras-chave no nome/descrição | Tipo |
|---|---|
| criar, nova página, landing page, captura, vendas | TIPO 1 — Criar Landing Page |
| otimizar, CRO, taxa de conversão, melhorar, revisar | TIPO 2 — Diagnóstico CRO |
| rastreamento, pixel, GTM, tag, evento, conversão | TIPO 3 — Configuração de Rastreamento |
| velocidade, PageSpeed, performance, Core Web Vitals | TIPO 4 — Otimização de Performance |
| brief, especificação, wireframe, escopo | TIPO 5 — Brief de Desenvolvimento |

## Buscar contexto do cliente

Se task tiver campo `Cliente` (list_relationship):
```
clickup_get_task(cliente_task_id)
```
Extrair: nicho, produto, identidade de marca (se disponível).

## Output
```
briefing:
  tipo: "TIPO 1 | 2 | 3 | 4 | 5"
  cliente: "[nome]"
  nicho: "[segmento]"
  objetivo: "[o que a página precisa fazer]"
  plataforma: "Next.js | WordPress | Webflow | a definir"
  url_atual: "[se for otimização/rastreamento]"
  referencias: "[links ou arquivos anexados]"
  copy_existe: true | false
  identidade_existe: true | false
```
