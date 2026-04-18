# Checklist de Entrega — Desenvolvimento Web

## Landing Page (TIPO 1)

### Estrutura e copy
- [ ] Todas as seções do tipo de página presentes
- [ ] H1 único, claro e com proposta de valor
- [ ] CTA presente no mínimo 2x (hero + seção final)
- [ ] FAQ trata objeções reais do público
- [ ] Prova social incluída (depoimentos, números, logos)

### Código
- [ ] Build sem erros: `npm run build`
- [ ] Sem TypeScript errors: `npx tsc --noEmit`
- [ ] Sem cores hardcoded — só `var(--color-*)`
- [ ] `FadeContent` em todas as seções
- [ ] Imagens com `alt` descritivo
- [ ] Semântica HTML correta
- [ ] `'use client'` apenas onde necessário

### Performance
- [ ] next/image em todas as imagens
- [ ] Fontes via `next/font/google`
- [ ] Sem imports desnecessários no bundle
- [ ] PageSpeed estimado > 80

### Mobile
- [ ] Testado em 375px (iPhone SE)
- [ ] Fontes legíveis em mobile (mínimo 16px corpo)
- [ ] Botões com área de toque mínima 44px
- [ ] Sem scroll horizontal

### Rastreamento
- [ ] UTMs capturadas via `useEffect` + `sessionStorage`
- [ ] Pixel Meta referenciado no briefing (ou checklist de instalação gerado)
- [ ] Evento de conversão apontado no CTA

### Deploy (Vercel)
- [ ] `.env.example` com todas as vars documentadas
- [ ] `vercel.json` com headers de segurança (se necessário)
- [ ] Domínio customizado instruído

## Diagnóstico CRO (TIPO 2)

- [ ] Problemas identificados com evidência concreta
- [ ] Cada problema tem correção específica e acionável
- [ ] Testes A/B definidos com KPI mensurável
- [ ] Próximos passos em ordem de impacto

## Rastreamento (TIPO 3)

- [ ] Passo a passo de instalação completo
- [ ] Checklist de verificação incluído
- [ ] Instruções de teste (Events Manager / Tag Assistant)
