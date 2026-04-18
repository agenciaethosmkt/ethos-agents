---
step: "05"
name: "Entregar Roteiro"
type: agent
agent: ogilvy
execution: inline
depends_on: step-04
---

# Step 05 — Ogilvy: Entregar Roteiro

## Para o Pipeline Runner

Ogilvy entrega o roteiro aprovado em 3 ações: roteiro na descrição da task,
legenda no campo personalizado e comentário de aviso.

## Parte A — Atualizar descrição da task com o roteiro

```
clickup_update_task(task_id,
  description = [roteiro completo de output/roteiro.md]
)
```

Formatar a descrição em markdown legível no ClickUp:
- `**[CENA 1] — 3s**` para títulos de cena
- `VISUAL:` / `VOZ OFF:` / `TEXTO NA TELA:` em linhas separadas
- Linha em branco entre cenas
- Seções "Áudio", "Notas de Produção" ao final

## Parte B — Preencher campo personalizado "Legenda"

```
clickup_update_task(task_id,
  custom_fields = {
    "Legenda": [legenda do post de output/roteiro.md — máximo 150 chars visíveis]
  }
)
```

Apenas o texto da legenda vai neste campo — sem hashtags (hashtags ficam nas notas de produção).

## Parte C — Comentar aviso de conclusão

```
clickup_create_task_comment(task_id,
  "🎬 Roteiro de Reels gerado.\n\n
  ▸ Duração estimada: Xs | Cenas: N\n
  ▸ Áudio sugerido: [áudio]\n
  ▸ Legenda preenchida no campo personalizado\n\n
  ✅ Roteiro na descrição. Aguardando aprovação para produção.")
```

## Parte D — Atualizar status

```
clickup_update_task(task_id, status="em revisão")
```

## Parte E — Atualizar memória

Registrar em `_memory/memories.md`:
- Arco narrativo usado e duração do vídeo
- Se houve ciclo de revisão e motivo
- Restrições de produção reveladas pelo briefing
