---
step: "03"
name: "Aprovação do Agendamento"
type: checkpoint
depends_on: step-02
---

# Step 03 — Checkpoint: Aprovação da Mensagem de Agendamento

## Para o Pipeline Runner

Apresentar a mensagem redigida pela Maya para aprovação humana antes do envio.
**Nenhuma mensagem é enviada sem aprovação explícita.**

---

Revisar a mensagem em `output/mensagem-agendamento.md`.

**A mensagem está aprovada para envio?**

1. Aprovar e enviar — Maya envia via WhatsApp agora
2. Ajustar o texto — descreva o que mudar
3. Mudar os horários sugeridos — informe as opções corretas
4. Cancelar — o CS vai entrar em contato manualmente

Se aprovada (opção 1), Maya enviará via protocolo WhatsApp e registrará na task.
