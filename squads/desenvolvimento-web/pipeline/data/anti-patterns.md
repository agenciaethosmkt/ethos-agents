# Anti-padrões & Padrões de Qualidade — Desenvolvimento Web

## Princípio central

Toda página entregue pela Ethos deve ter **UX premium** — não apenas funcional, mas visualmente sofisticada e fluida. Isso inclui uso de recursos externos de design de alto nível.

---

## Bancos externos obrigatórios

### Imagens e visuais

| Recurso | Uso | URL |
|---|---|---|
| **Unsplash** | Fotos de alta resolução gratuitas | unsplash.com |
| **Pexels** | Fotos e vídeos gratuitos | pexels.com |
| **StockSnap** | Fotos lifestyle e negócios | stocksnap.io |
| **Freepik** | Ilustrações, mockups, vetores | freepik.com |
| **unDraw** | Ilustrações SVG por cor (personalizável) | undraw.co |

### Ícones

| Recurso | Uso | Como usar |
|---|---|---|
| **Lucide React** | Ícones consistentes — padrão do stack | `import { Icon } from 'lucide-react'` |
| **React Icons** | Biblioteca ampla (Font Awesome, Material, etc.) | `import { FaIcon } from 'react-icons/fa'` |
| **Heroicons** | Ícones Tailwind oficiais | via React Icons |
| **Phosphor Icons** | Ícones modernos e variados | via React Icons |

### Animações prontas

| Recurso | Uso | Como usar |
|---|---|---|
| **LottieFiles** | Animações JSON vetoriais (loading, success, etc.) | lottiefiles.com → `lottie-react` |
| **Framer Motion** | Animações de entrada, hover, scroll | `motion/react` |
| **AOS** | Animate on scroll para seções | inicializar no layout.tsx |

### Gradientes e backgrounds

| Recurso | Uso | URL |
|---|---|---|
| **Mesh Gradient** | Gradientes mesh para hero backgrounds | meshgradient.in |
| **Haikei** | SVG waves, blobs, formas orgânicas | haikei.app |
| **CSS Gradient** | Gradientes lineares/radiais | cssgradient.io |
| **Grainy Gradient** | Gradientes com textura grain | css.glass / shadergradient.co |

### Tipografia

| Recurso | Uso | Como usar |
|---|---|---|
| **Google Fonts** | Fontes web otimizadas | `next/font/google` |
| **Fontshare** | Fontes premium gratuitas | fontshare.com → download + `next/font/local` |

---

## Padrões UX Premium obrigatórios

### Visual
- **Gradientes sutis** no hero — nunca fundo liso sem textura
- **Glassmorphism** em cards: `backdrop-blur + bg-white/10 + border border-white/20`
- **Sombras com cor** (não apenas cinza): `shadow-[0_20px_60px_rgba(var(--accent-rgb),0.15)]`
- **Micro-interações** em botões: scale + shine via Framer Motion
- **Imagens com lazy load** via `next/image` com placeholder blur

### Tipografia
- Nunca usar fonte padrão do sistema — sempre Google Fonts ou Fontshare
- Hierarquia clara: heading bold/black + body regular + caption light
- Espaçamento generoso: `leading-tight` em headlines, `leading-relaxed` em corpo

### Animações
- FadeContent com blur em seções de destaque: `<FadeContent blur delay={200}>`
- Delay sequencial em listas/grids (não animação simultânea): `delay={i * 60 + 150}`
- Hover em cards: `whileHover={{ y: -4, scale: 1.01 }}` + transição spring
- Nenhuma seção aparece estática — tudo anima no scroll

### Layout
- Seções com espaçamento vertical generoso: `py-20 md:py-32`
- Max-width consistente: `max-w-6xl mx-auto px-4 md:px-8`
- Grid responsivo: `grid-cols-1 md:grid-cols-2 lg:grid-cols-3`

---

## Nunca fazer

- **Fundo liso sem textura/gradiente** no hero — parece amador
- **Ícones emoji** em lugar de ícones do Lucide/React Icons
- **Imagens sem otimização** — sempre `next/image` com `width`, `height` e `alt`
- **Cores hardcoded** — sempre `var(--color-*)`
- **Dois CTAs diferentes** — um objetivo, um botão
- **Animações simultâneas** em itens de lista — usar delay sequencial
- **Mobile ignorado** — testar em 375px obrigatoriamente
- **Página sem pixel** antes de publicar

---

## Cenários de erro

| Situação | Ação |
|---|---|
| Copy não existe | Criar subtask para Ogilvy, abortar pipeline |
| Identidade visual não existe | Usar paleta genérica Ethos + solicitar ao cliente |
| URL inacessível (CRO/rastreamento) | Solicitar acesso ou screenshot |
| Cliente sem nicho definido | Perguntar antes de escolher fontes/paleta |
| Lottie muito pesado (>500kb) | Usar versão comprimida ou substituir por Framer Motion |
