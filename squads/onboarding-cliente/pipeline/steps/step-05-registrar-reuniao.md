---
step: "05"
name: "Registrar Reunião"
type: checkpoint
depends_on: step-04
outputFile: output/notas-reuniao.md
---

# Step 05 — Checkpoint: Registrar Informações da Reunião

## Para o Pipeline Runner

A reunião foi realizada pelo CS. Agora o humano preenche as informações coletadas
para que o Redator possa montar os próximos passos e a passagem interna.

**Se persona = eletricistas:** este step registra o retorno do formulário de briefing, não de uma reunião.

---

A reunião de onboarding foi realizada. Preencha as informações abaixo:

**1. Contexto atual do negócio do cliente**
(o que ele faz, como funciona, tamanho, situação atual)

**2. Principais objetivos do cliente com a Ethos**
(o que ele espera alcançar)

**3. Prioridades iniciais**
(o que precisa ser feito PRIMEIRO, o que é mais urgente)

**4. Ofertas e serviços prioritários**
(quais produtos/serviços do cliente serão trabalhados primeiro)

**5. Restrições e pontos sensíveis**
(o que NÃO fazer, limitações, experiências ruins anteriores)

**6. Responsáveis por aprovações**
(quem aprova conteúdo, campanhas, artes — nome e contato)

**7. Observações livres**
(qualquer informação relevante que não se encaixa acima)

---

As informações serão salvas em `output/notas-reuniao.md` e usadas para montar
os próximos passos e a passagem interna para as áreas.
