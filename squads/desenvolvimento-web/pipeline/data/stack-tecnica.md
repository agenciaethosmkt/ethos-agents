# Stack Técnica — Desenvolvimento Web Ethos

## Stack principal (novos projetos)

| Camada | Tecnologia | Versão |
|---|---|---|
| Framework | Next.js App Router | 15 |
| Linguagem | TypeScript | 5 (strict mode) |
| Estilo | Tailwind CSS | 4 (via @tailwindcss/postcss) |
| Componentes | shadcn/ui | new-york style |
| Animações | Framer Motion | 12 (import via motion/react) |
| Scroll animado | AOS | 2.3.4 |
| Smooth scroll | Lenis | latest |
| Ícones | Lucide React + React Icons | latest |
| Carrossel | Embla Carousel | latest |
| Deploy | Vercel | — |

## Instalação base

```bash
npx create-next-app@latest projeto --typescript --tailwind --app --src-dir --import-alias "@/*"
cd projeto
npx shadcn@latest init
npm install framer-motion aos lenis lucide-react react-icons embla-carousel-react
```

## Estrutura de pastas

```
src/
├── app/
│   ├── layout.tsx          # Lenis + AOS init + fonts
│   ├── globals.css         # Variáveis CSS + Tailwind import
│   └── (public)/
│       └── [slug]/
│           └── page.tsx
├── components/
│   ├── ui/
│   │   ├── FadeContent.tsx
│   │   └── ButtonCTA.tsx
│   └── pages/
│       └── [slug]/
│           ├── Hero.tsx
│           ├── Beneficios.tsx
│           ├── Depoimentos.tsx
│           ├── FAQ.tsx
│           └── CTAFinal.tsx
└── lib/
    └── utils.ts
```

## Regras não-negociáveis

- Mobile-first: CSS base para mobile, breakpoints `md:` e `lg:`
- Nunca cores hardcoded: sempre `var(--color-*)` via Tailwind `bg-[var(--color-card)]`
- `FadeContent` em toda seção
- `'use client'` apenas onde há hooks, eventos ou motion
- `framer-motion` sempre via `motion/react` (não `framer-motion` direto)
- Imagens sempre com `alt` descritivo
- Semântica HTML: `<section>`, `<article>`, `<nav>`, `<header>`, `<footer>`

## Plataformas secundárias

- **WordPress + Elementor** — clientes com site existente
- **WebFlow** — quando cliente já usa a plataforma
- **HTML estático** — landing pages simples sem backend
