---
step: "03"
name: "Redigir Conteúdo da Proposta"
type: agent
agent: redator
inputFiles:
  - output/diagnostico.md
  - output/case-selecionado.md
outputFile: output/conteudo-proposta.md
---

# Step 03 — Redigir Conteúdo da Proposta

## Estrutura obrigatória (ordem que converte)

A proposta não começa falando sobre a Ethos — começa falando sobre o lead.

---

### Seção 1 — Hero (capa personalizada)

```
Título: "[Nome do lead], vamos transformar [dor principal] em [resultado esperado]?"
Subtítulo: "Proposta Ethos — [Plano] — [Mês/Ano]"
```

**Nunca:** "Proposta Comercial — Gestão de Marketing"

---

### Seção 2 — "Entendemos o seu desafio"

Diagnóstico em 3 bullets usando as palavras do próprio lead (da transcrição Tactiq):

```
✓ [dor 1 — de preferência uma frase que o lead disse na reunião]
✓ [dor 2]
✓ [dor 3]
```

Finalizar com: "É exatamente para resolver isso que a Ethos existe."

---

### Seção 3 — Resultado esperado

Específico, mensurável, com prazo:

```
Nos primeiros [X meses] com a Ethos, você vai:
→ [resultado 1 concreto — ex: "sair de X para Y leads/mês"]
→ [resultado 2]
→ [resultado 3]
```

---

### Seção 4 — Como a Ethos resolve (máx. 3 pilares)

Cada pilar com nome + 2 linhas de descrição.
Baseado no plano sugerido (Flow/Growth).

Ver `pipeline/data/pilares-por-plano.md` para os pilares de cada plano.

---

### Seção 5 — Prova social

Usar o case do output/case-selecionado.md:

```
[Nome ou "Um [segmento] em [cidade]"] tinha [situação inicial].
Após [X meses] com a Ethos: [resultado mensurável].
```

Se possível: foto ou logo do cliente (com permissão).

---

### Seção 6 — O que está incluído

Tabela de entregas baseada no plano contratado.
Ver `pipeline/data/planos-ethos.md` para o escopo de cada plano.

---

### Seção 7 — Equipe responsável

2–3 pessoas com nome, foto (se disponível) e papel.
Padrão: Renato Cristiano (Estratégia) + [gestor responsável] + [designer/copywriter].

---

### Seção 8 — Cronograma de início

3 etapas visuais:
```
Semana 1: Onboarding e briefing completo
Semana 2: Estruturação e acessos
Semana 3: Primeiras ações ao vivo
```

---

### Seção 9 — Investimento

```
[Nome do Plano]
R$ [valor]/mês

Inclui: [lista resumida de 3–4 itens]

Prazo mínimo: [X meses]
Início: mediante assinatura do contrato
```

**Ancoragem de valor:** logo acima do preço, inserir:
> "Clientes Ethos no plano [X] geram em média [Y leads/mês] com custo de aquisição [Z% abaixo da média do setor]."

---

### Seção 10 — CTA

```
[Botão] "Quero começar"
[Texto] "Dúvidas? Fale com Renato → [WhatsApp]"
"Proposta válida até [data + 7 dias]"
```

---

## Regras de escrita

- Usar o nome do lead pelo menos 3 vezes na proposta (personalização percebida)
- Cada seção: máximo 60 palavras (proposta é para ler, não estudar)
- Números concretos > adjetivos vagos ("3x mais leads" > "muito crescimento")
- Nunca mencionar concorrentes
- Nunca prometer resultado garantido — usar "clientes similares alcançaram"

## Output — salvar em output/conteudo-proposta.md

Estruturar o conteúdo seção por seção, pronto para ser inserido no Gamma.
