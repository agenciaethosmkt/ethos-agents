# Step 03 — Executar Desenvolvimento

## Agente
desenvolvedor

## Objetivo
Executar o trabalho principal com base no tipo identificado no step-01.

---

## TIPO 1 — Criar Landing Page

Usar skill `agente-landing-page`:

### Wizard de identidade (coletar da task / CRM / briefing)
1. Nicho/segmento do cliente
2. Tema: dark | light | misto
3. Cor principal (hex ou da identidade visual)
4. Cor do CTA
5. Tom tipográfico: serifada | sans-serif | display

### Estrutura a gerar

Baseado no objetivo:

| Objetivo | Tipo de página | Seções obrigatórias |
|---|---|---|
| Captura de lead | `captura` | Hero+form → Benefícios → CTA reforçado |
| Venda direta | `vendas` | Hero → Problema → Solução → Benefícios → Prova Social → Garantia → FAQ → CTA Final |
| Apresentação | `institucional` | Hero → Sobre → Serviços → Cases → Depoimentos → Contato |

### Output esperado

Para sessão de desenvolvimento ativo (Claude Code CLI):
- Estrutura completa de componentes Next.js
- `globals.css` com variáveis do cliente
- `page.tsx` montado
- Cada seção como componente separado em `components/pages/`

Para entrega de especificação (desenvolvedor humano):
- Usar skill `47-design-ui-ux` → wireframe textual + specs de cada componente

---

## TIPO 2 — Diagnóstico CRO

Analisar a página a partir dos dados disponíveis (URL, taxa de conversão, screenshots se anexados):

1. Avaliar headline — clareza, proposta de valor, impacto
2. Avaliar CTA — visibilidade, texto, posicionamento
3. Avaliar estrutura — fluxo lógico, prova social, objeções tratadas
4. Avaliar técnico — velocidade, mobile, rastreamento

Gerar relatório de diagnóstico conforme formato em `data/checklist-entrega.md`.

---

## TIPO 3 — Configuração de Rastreamento

Gerar passo a passo técnico para:
- Instalação do Pixel Meta via GTM
- Configuração de eventos (Lead, Purchase, PageView)
- Verificação via Events Manager / Tag Assistant

---

## TIPO 4 — Otimização de Performance

Analisar relatório PageSpeed (se fornecido) e gerar:
- Lista de problemas por prioridade
- Correções técnicas específicas (next/image, lazy load, font subsetting)
- Estimativa de ganho por correção

---

## TIPO 5 — Brief de Desenvolvimento

Usar skill `44-design-briefing` para gerar:
- Escopo detalhado do projeto
- Referências visuais estruturadas
- Specs técnicas (plataforma, integrações, prazo)
- Critérios de aprovação
