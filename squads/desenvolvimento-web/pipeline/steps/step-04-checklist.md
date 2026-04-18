# Step 04 — Checklist de Qualidade

## Agente
revisor

## Objetivo
Validar a entrega antes de publicar no ClickUp.

## Checklist por tipo

### TIPO 1 — Landing Page criada

**Estrutura:**
- [ ] Todas as seções obrigatórias do tipo de página presentes
- [ ] Hierarquia visual clara: H1 → H2 → corpo
- [ ] CTA aparece no mínimo 2x (hero + final)
- [ ] FAQ trata as principais objeções

**Código (se gerado):**
- [ ] `'use client'` apenas onde necessário
- [ ] Sem cores hardcoded — apenas `var(--color-*)`
- [ ] `FadeContent` em todas as seções
- [ ] Imagens com `alt` descritivo
- [ ] Semântica HTML correta (`<section>`, `<header>`, `<footer>`)
- [ ] Mobile-first nos estilos Tailwind

**Performance:**
- [ ] next/image para todas as imagens
- [ ] Fontes via `next/font/google`
- [ ] Sem imports desnecessários

**Rastreamento:**
- [ ] UTMs sendo capturadas no `useEffect`
- [ ] Evento de conversão apontado no CTA principal

### TIPO 2 — Diagnóstico CRO

- [ ] Problemas identificados com evidência (não apenas opinião)
- [ ] Cada problema tem correção específica
- [ ] Testes A/B recomendados são testáveis
- [ ] Próximos passos ordenados por impacto

### TIPO 3 — Rastreamento

- [ ] Checklist completo de instalação gerado
- [ ] Instruções de verificação incluídas
- [ ] Não dependente de acesso ao servidor (GTM preferred)

## Veto conditions — bloquear entrega se:

- Página sem nenhum CTA
- Código com `console.log` em produção
- Imagens sem `alt`
- Copy genérico sem adaptação ao cliente
- Checklist técnico com mais de 2 itens críticos em aberto

## Output
Checklist validado com status de cada item. Ajustes necessários apontados para o desenvolvedor.
