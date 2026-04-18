---
step: "02"
name: "Identificar Campanhas"
type: agent
agent: analista
---

# Step 02 — Identificar Campanhas

## Objetivo

Mapear as campanhas ativas/pausadas do período para saber exatamente o que será analisado.

## Buscar tasks de campanha vinculadas

```
clickup_get_task(task_id) → task.links → filtrar tasks de "Gestão de Campanhas"
```

Para cada task de campanha vinculada:
```
clickup_get_task(campanha_task_id) → extrair:
- task.name           → nome da campanha
- custom_fields["ID da Campanha"]  → ID na plataforma (Meta/Google)
- custom_fields["Canal"]           → Meta | Google | etc
- custom_fields["Objetivo"]        → conversão | tráfego | alcance | etc
- custom_fields["Verba"]           → orçamento da campanha
- custom_fields["Data de Início"]  → data de início
- custom_fields["Data de Fim"]     → data de encerramento (se aplicável)
```

## Salvar mapa de campanhas

```markdown
## Campanhas identificadas para o relatório

| ID | Nome | Plataforma | Objetivo | Verba | Período |
|---|---|---|---|---|---|
| {id} | {nome} | {plataforma} | {objetivo} | R$ {verba} | {início} → {fim} |
```

## Se não houver tasks vinculadas

Prosseguir com busca direta na API usando:
- Nome do cliente como referência
- Período definido no step-01
- Registrar no relatório: "campanhas identificadas via API, sem task vinculada"
