# Step 02 — Verificar Pré-requisitos

## Agente
estrategista

## Objetivo
Garantir que todos os insumos necessários existem antes de iniciar o desenvolvimento.

## Pré-requisitos por tipo

### TIPO 1 — Criar Landing Page
- [ ] **Objetivo** — captura / venda / agendamento / institucional
- [ ] **Público** — quem é o ICP da página
- [ ] **CTA único** — 1 ação principal definida
- [ ] **Copy** — headline, corpo, depoimentos, FAQ
- [ ] **Identidade visual** — paleta de cores, fontes, referências

### TIPO 2 — Diagnóstico CRO
- [ ] **URL da página** atual
- [ ] **Taxa de conversão** atual ou meta
- [ ] **Fonte de tráfego** principal

### TIPO 3 — Rastreamento
- [ ] **URL da página**
- [ ] **Plataforma de anúncios** (Meta / Google / ambos)
- [ ] **Evento de conversão** a rastrear (Lead / Purchase / outro)

### TIPO 4 — Performance
- [ ] **URL da página**
- [ ] **Score atual** no PageSpeed (se disponível)

### TIPO 5 — Brief
- [ ] **Objetivo** da página
- [ ] **Plataforma** de desenvolvimento
- [ ] **Prazo** e escopo

## Se pré-requisito crítico estiver faltando

**Copy não existe (TIPO 1):**
```
clickup_create_task(
  name="[Copy] [Nome da página] — {task.name}",
  list_id=<lista Processo de Copywriting>,
  description="Copy necessário para a landing page: {task.name}\nObjetivo: {objetivo}\nPúblico: {publico}\nCTA: {cta}",
  assignees=[ogilvy_user_id]
)
clickup_create_task_comment(
  task_id=task.id,
  comment_text="⏸️ LaryPages: aguardando copy da página.\nSubtask criada para o Ogilvy: [link]\nVoltarei a executar quando o copy estiver aprovado.",
  notify_all=true
)
clickup_update_task(task_id=task.id, status="aguardando")
```
→ **ABORTAR** pipeline até copy disponível.

**Identidade visual não existe (TIPO 1):**
```
clickup_create_task_comment(
  task_id=task.id,
  comment_text="⚠️ LaryPages: identidade visual não encontrada.\nNecessário: paleta de cores, fontes, referências visuais.\nPor favor, adicione na descrição ou anexe na task.",
  notify_all=true
)
```
→ Continuar com identidade genérica da Ethos se urgente, ou aguardar.

## Output
Pré-requisitos validados → prosseguir para step-03.
Pré-requisito crítico faltando → abortar com subtask + comentário.
