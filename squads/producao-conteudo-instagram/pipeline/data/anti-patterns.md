# Anti-patterns — Erros Comuns a Evitar

## Copy

### ❌ Ganchos fracos
```
❌ "Você sabia que o Instagram pode ajudar seu negócio?"
❌ "Hoje vou compartilhar algumas dicas..."
❌ "Olá, tudo bem? Hoje falaremos sobre..."
✅ "Você está perdendo clientes por causa desse erro simples."
✅ "3 erros que toda empresa comete no Instagram (e como parar agora)."
```

### ❌ CTAs vagos
```
❌ "Me conta nos comentários!"
❌ "Curte se concordar!"
✅ "Comenta 'QUERO' e te mando o checklist grátis."
✅ "Salva esse post — você vai precisar dele."
```

### ❌ Hashtags genéricas
```
❌ #marketing #business #empreendedorismo #sucesso #motivacao
✅ #marketingdigitalbrasil #instagramparaempresas #gestaoderedes
```

### ❌ Tom errado por cliente
- Clínica médica: nunca usar gírias ou humor forçado
- Marca jovem: nunca usar linguagem formal e distante
- Sempre ler o briefing do cliente antes de escrever

---

## Design

### ❌ Texto pequeno demais
- Nunca abaixo de 20px equivalente
- Sempre simular como ficaria em tela de celular pequeno

### ❌ Informação demais em um post
- Post de feed: máximo 1 ideia principal + 1 CTA
- Não tentar colocar 5 pontos em um único slide

### ❌ Criar sem brand kit
- Sempre buscar brand kit no Canva antes de criar
- Se não encontrar: perguntar antes de usar template genérico

### ❌ Alterar a copy do Ogilvy
- O Designer não edita copy
- Se houver problema de espaço: reportar ao Revisor, não cortar texto

---

## Agendamento

### ❌ Usar start_date para publicação
- O campo que aciona o Make é o `due_date`
- `start_date` é usado APENAS na lista "Envio de Mensagens"

### ❌ Agendar formato manual sem comentário
- Stories, Reels e YouTube precisam de comentário com instruções
- Nunca marcar "Agendado" sem comentário nesses formatos

---

## Geral

### ❌ Processar task já processada
- Sempre verificar tag `agente-processado` antes de iniciar
- Se tag presente: parar imediatamente, não duplicar

### ❌ Avançar fase sem aprovação de Renato
- Copy → Design: aguardar aprovação (automação muda a lista)
- Design → Agendamento: aguardar aprovação (automação muda a lista)
- Nunca pular as revisões humanas
