---
step: "06"
name: "Próximos Passos"
type: agent
agent: redator
execution: inline
depends_on: step-05
inputFile: output/notas-reuniao.md
outputFile: output/proximos-passos.md
---

# Step 06 — Redator: Documento de Próximos Passos

## Para o Pipeline Runner

O Redator monta o documento de próximos passos para enviar ao cliente — o que acontece agora,
o que ele precisa fazer e o que a Ethos vai fazer nos primeiros dias.

## Inputs

- `output/notas-reuniao.md` — informações coletadas na reunião
- `output/validacao.yaml` — plano e dados do cliente
- `pipeline/data/checklist-onboarding.md` — checklist padrão por plano

## Processo

1. Ler notas da reunião e identificar prioridades
2. Montar os 3 blocos de próximos passos: Briefing, Acessos, Setup
3. Adaptar ao plano do cliente (checklists específicos por plano)
4. Redigir em tom claro e direto para o cliente

## Output esperado

Salvar em `output/proximos-passos.md`:

```markdown
# Próximos Passos — [Cliente] — [Plano]

Olá, [nome]! Aqui estão os próximos passos para darmos início ao seu projeto.

## 📋 Briefing
[link ou instruções para preenchimento do briefing estratégico]
Prazo: [data]

## 🔑 Acessos
Os seguintes acessos precisam ser liberados para a nossa equipe:
- [ ] [acesso 1] — como liberar: [instrução]
- [ ] [acesso 2]
- [ ] [acesso 3]
Prazo: [data]

## ⚙️ Setup
Após os acessos, nossa equipe irá:
- [ ] [ação 1]
- [ ] [ação 2]
Previsão: [prazo]

## 📅 Próxima conversa
[quando e como será o próximo contato]

---
Qualquer dúvida, pode chamar aqui no WhatsApp. Estamos à disposição! 🚀
```

## Veto Conditions

- Documento sem os 3 blocos (Briefing, Acessos, Setup) → rejeitar
- Tom genérico sem nome do cliente → rejeitar
- Sem prazos definidos → alertar (pode deixar em branco se CS não informou)
