---
step: "01"
name: "Briefing"
type: checkpoint
outputFile: output/briefing.yaml
---

# Step 01 — Briefing do Criativo

## Para o Pipeline Runner

Coletar o briefing completo do criativo. Os dados vêm da **task do ClickUp** que acionou o squad.

Ler `task.description` e `task.custom_fields[]` e preencher o briefing abaixo.
Se algum campo obrigatório estiver ausente: listar os campos faltantes e aguardar preenchimento humano antes de prosseguir.

## Campos obrigatórios

| Campo | Onde buscar | Exemplo |
|---|---|---|
| `cliente` | Custom field "Cliente" | Kassio Galdino |
| `produto` | Descrição da task | Mentoria de Finanças |
| `objetivo` | Custom field "Objetivo" | Geração de leads |
| `plataforma` | Custom field "Plataforma" | Meta Ads |
| `formato` | Custom field "Formato" | Imagem estática / Vídeo / Carrossel |
| `publico` | Descrição da task | Mulheres 30-45, interessadas em investimentos |
| `orcamento_diario` | Custom field ou task de campanha linkada | R$ 50/dia |

## Campos opcionais (enriquecem o resultado)

| Campo | Onde buscar |
|---|---|
| `angulo_sugerido` | Descrição da task (se o humano já indicou um ângulo) |
| `referencias` | Links ou nomes de criativos de referência na task |
| `tom` | Custom field "Tom de voz" |
| `oferta` | Descrição — o que exatamente está sendo anunciado |
| `task_campanha_id` | ID da task de campanha linkada (vinda do Sobral) |
| `historico_criativos` | Se existir doc de histórico, resumir o que já foi testado |

## Output esperado

Salvar em `output/briefing.yaml`:

```yaml
cliente: ""
produto: ""
objetivo: ""       # leads / vendas / awareness / tráfego
plataforma: ""     # Meta Ads / Google Ads / Ambos
formato: ""        # imagem / video / carrossel / story
publico: ""
orcamento_diario: ""
angulo_sugerido: ""
referencias: []
tom: ""
oferta: ""
task_campanha_id: ""
historico_criativos: ""
origem: ""         # Sobral / Kizo
```

## Se campos obrigatórios estiverem ausentes

```
clickup_update_task(task_id, status="em alteração & ajustes")
clickup_create_task_comment(task_id,
  "🔍 Criativo não iniciado — campos obrigatórios ausentes:\n\n▸ [campo]: [onde preencher]\n\nPreencha e reenvie para o agente.")
```
→ ABORTAR pipeline
