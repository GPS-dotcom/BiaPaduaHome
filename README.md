# Handoff: Site institucional — Bia Pádua Home

## Overview
Site institucional de página única para a Bia Pádua Home, marca de têxteis sob medida (almofadas, colchas, cortinas, persianas e tapeçaria) para clientes de alto padrão. Não é e-commerce: é uma vitrine editorial de projetos realizados, sem preços, sem carrinho e sem CTA comercial. Seções: header fixo, hero em tela cheia, grid de projetos com galeria em overlay, "Sobre" e footer com contato.

## About the Design Files
Os arquivos deste pacote são **referências de design feitas em HTML** — protótipos que mostram aparência e comportamento pretendidos, não código de produção para copiar direto. A tarefa é **recriar esses designs no ambiente do codebase de destino** (Next.js/React, Astro, Vue, etc.), usando os padrões e bibliotecas já estabelecidos ali. Se não existir codebase, recomenda-se Next.js (App Router) ou Astro — o site é estático, orientado a imagens, e se beneficia de `next/image` ou do pipeline de imagens do Astro.

## Fidelity
**Alta fidelidade (hifi)** para layout, tipografia, cor, espaçamento e microinterações: os valores abaixo são finais e devem ser reproduzidos fielmente.
Exceção: **as imagens são placeholders**. No protótipo cada imagem é um `<image-slot>` (componente de placeholder arrastável do ambiente de design). Na implementação real, substituir cada slot por `<img>`/`<picture>` (ou `next/image`) com a fotografia definitiva do projeto, `object-fit: cover`, `loading="lazy"` (exceto o hero, que deve ser `priority`/eager) e `alt` descritivo.

## Screens / Views

### 1. Header (fixo, global)
- **Purpose**: navegação mínima e assinatura da marca.
- **Layout**: `position: fixed; top/left/right: 0; z-index: 40; display: flex; align-items: center; justify-content: space-between; gap: 24px; padding: 22px clamp(20px, 5vw, 64px)`.
- **Truque visual**: `mix-blend-mode: difference` + `color: #F7F4EF`. O header se inverte automaticamente sobre foto escura (hero) e sobre fundo creme (resto da página) — não há troca de tema por scroll. Se o codebase não suportar blend mode de forma confiável, alternativa: trocar a cor do texto via IntersectionObserver no hero.
- **Componentes**:
  - Wordmark `<a href="#top">`: Marcellus, `clamp(15px, 2.2vw, 19px)`, `letter-spacing: 0.26em`, uppercase. Texto: "Bia Pádua Home" — a palavra "Home" em `opacity: 0.6`.
  - Nav: flex, `gap: clamp(18px, 3vw, 40px)`, itens Jost 11.5px / `letter-spacing: 0.22em` / uppercase / `opacity: 0.85`, hover `opacity: 1`. Itens: "Projetos" (#projetos), "Sobre" (#sobre), "Contato" (#contato).

### 2. Hero (`#top`)
- **Purpose**: primeira impressão e posicionamento da marca, sem CTA.
- **Layout**: `height: 100svh; min-height: 560px; overflow: hidden; background: #262523`. Imagem absoluta preenchendo `inset: 0`.
- **Scrim**: `linear-gradient(180deg, rgba(38,37,35,0.42) 0%, rgba(38,37,35,0.06) 42%, rgba(38,37,35,0.5) 100%)`, `pointer-events: none`.
- **Bloco de texto**: absoluto, `left/right: clamp(20px, 5vw, 64px)`, `bottom: clamp(64px, 10vh, 120px)`, flex column, `gap: 18px`, `pointer-events: none`.
  - Eyebrow: "Tapeçaria sob medida" — Jost 10.5px, `letter-spacing: 0.34em`, uppercase, `rgba(247,244,239,0.72)`.
  - H1: "O têxtil como estrutura do ambiente." — Marcellus 400, `clamp(30px, 5.4vw, 62px)`, `line-height: 1.12`, `max-width: 15em`, `color: #F7F4EF`, `text-wrap: pretty`.
- **Variante**: existe uma opção de texto centralizado (align/justify center, `inset` vertical 0). Padrão é inferior-esquerdo.

### 3. Projetos (`#projetos`)
- **Purpose**: portfólio editorial; cada card abre a galeria daquele ambiente.
- **Section padding**: `clamp(72px, 12vh, 150px) clamp(20px, 5vw, 64px) clamp(40px, 6vh, 80px)`.
- **Cabeçalho da seção**: linha flex-wrap com `justify-content: space-between`, `border-bottom: 1px solid #E3DCD2`, `padding-bottom: 22px`, `margin-bottom: clamp(36px, 6vh, 72px)`.
  - H2 "Projetos": Marcellus 400, `clamp(24px, 3.4vw, 38px)`.
  - Parágrafo (max 34ch, 13.5px, `line-height: 1.7`, `#6E6A63`): "Ambientes realizados em residências e apartamentos, com peças desenvolvidas exclusivamente para cada espaço."
- **Grid**: `grid-template-columns: repeat(auto-fit, minmax(min(100%, 320px), 1fr)); gap: clamp(28px, 4vw, 56px) clamp(20px, 3vw, 40px)`. Dois cards ocupam `grid-column: span 2` (Casa Serra do Cipó, Residência Alphaville) → ritmo assimétrico; em mobile o `min(100%, …)` colapsa para 1 coluna.
- **Card**: `cursor: pointer`. Caixa de imagem `position: relative; overflow: hidden; background: #EDE7DE`, aspect-ratio `16/10` nos cards largos e `4/5` nos estreitos. Imagem: `transition: transform 900ms cubic-bezier(0.16,1,0.3,1)`, hover `scale(1.035)` (a caixa recorta).
- **Legenda do card**: flex baseline space-between, `padding-top: 16px`.
  - Título: Marcellus 400, `clamp(18px, 1.6vw, 23px)`, `margin-bottom: 5px`.
  - Categorias: 11.5px, `letter-spacing: 0.18em`, uppercase, `#8C877E`.
  - Ano: 11.5px, `letter-spacing: 0.16em`, `#A8A29A` (ocultável).
- **Conteúdo dos 6 cards** (título · categorias · ano):
  1. Casa Serra do Cipó · Cortinas · Colchas · Almofadas · 2025 (largo)
  2. Apartamento Lourdes · Persianas · Cabeceira · 2025
  3. Suíte Belvedere · Colchas · Tapeçaria · 2024
  4. Residência Alphaville · Cortinas · Estofados · 2024 (largo)
  5. Cobertura Savassi · Almofadas · Persianas · 2023
  6. Casa Vale do Sereno · Tapeçaria · Cortinas · 2023

### 4. Galeria do projeto (overlay, uma por projeto)
- **Purpose**: ver as fotos de um ambiente realizado. Abre no clique do card.
- **Layout**: `position: fixed; inset: 0; z-index: 60; background: #F7F4EF; overflow-y: auto`; `body` com `overflow: hidden` enquanto aberta.
- **Barra sticky**: `top: 0`, `padding: 22px clamp(20px, 5vw, 64px)`, `background: rgba(247,244,239,0.92)`, `backdrop-filter: blur(8px)`, `border-bottom: 1px solid #E3DCD2`.
  - Título do projeto: Marcellus 400, `clamp(19px, 2.4vw, 27px)`.
  - Meta (cidade · ano): 11px, `letter-spacing: 0.2em`, uppercase, `#8C877E`.
  - Botão "Fechar": borda `1px solid #D7CFC3`, fundo transparente, Jost 10.5px, `letter-spacing: 0.22em`, uppercase, `padding: 11px 20px`, `transition: all 300ms ease`; hover `background #262523 / color #F7F4EF / border #262523`.
- **Grid de fotos**: `padding: clamp(28px, 5vw, 64px) clamp(20px, 5vw, 64px) clamp(64px, 10vh, 120px)`, `repeat(auto-fit, minmax(min(100%, 420px), 1fr))`, `gap: clamp(20px, 3vw, 40px)`, `max-width: 1500px`, centralizado. Cada figura: caixa `aspect-ratio: 3/2`, `overflow: hidden`, `background #EDE7DE`; figcaption `padding-top: 12px`, 11.5px, `letter-spacing: 0.16em`, uppercase, `#A8A29A`.
- **Dados** (title / meta / legendas) — 4 fotos por projeto:
  - `serra` — Casa Serra do Cipó · Nova Lima, MG · 2025 — "Sala de estar — cortinas em linho", "Almofadas em algodão e seda", "Varanda — colcha de verão", "Detalhe de acabamento manual"
  - `lourdes` — Apartamento Lourdes · Belo Horizonte, MG · 2025 — "Quarto principal — persianas romanas", "Cabeceira sob medida", "Estar íntimo", "Detalhe do tecido"
  - `belvedere` — Suíte Belvedere · Belo Horizonte, MG · 2024 — "Colcha e mantas", "Tapeçaria da poltrona", "Vista geral da suíte", "Detalhe do vivo em contraste"
  - `alphaville` — Residência Alphaville · Lagoa dos Ingleses, MG · 2024 — "Sala de jantar — cortinas até o piso", "Estofamento das cadeiras", "Hall de entrada", "Detalhe do bandô"
  - `savassi` — Cobertura Savassi · Belo Horizonte, MG · 2023 — "Varanda — almofadas em tons de areia", "Persianas de madeira", "Estar externo", "Detalhe da costura"
  - `vale` — Casa Vale do Sereno · Nova Lima, MG · 2023 — "Home theater — cortinas blackout", "Tapeçaria do sofá", "Detalhe de veludo", "Ambiente integrado"

### 5. Sobre (`#sobre`)
- **Layout**: `background: #F0EBE3`, `padding: clamp(80px, 14vh, 170px) clamp(20px, 5vw, 64px)`. Grid `repeat(auto-fit, minmax(min(100%, 340px), 1fr))`, `gap: clamp(40px, 6vw, 90px)`, `align-items: center`, `max-width: 1320px`, centralizado.
- **Coluna imagem**: `aspect-ratio: 3/4`, `overflow: hidden`, `background #E3DCD2` (retrato ou detalhe de tecido/ateliê).
- **Coluna texto** (`max-width: 46ch`, `gap: 22px`):
  - Eyebrow "Sobre": 10.5px, `letter-spacing: 0.34em`, uppercase, `#A0968A`.
  - H2 "Bia Pádua Home": Marcellus 400, `clamp(26px, 3.6vw, 42px)`, `line-height: 1.2`.
  - Dois parágrafos: 15.5px, `line-height: 1.85`, `#4A463F`, `text-wrap: pretty` (copy exata no HTML).
  - Trio de atributos: grid `repeat(auto-fit, minmax(140px, 1fr))`, `gap: 24px`, `border-top: 1px solid #DFD7CB`, `padding-top: 26px`. Cada item: título Marcellus 20px ("Sob medida", "Curadoria", "Instalação") + descrição 12.5px `line-height: 1.6` `#8C877E`.

### 6. Footer (`#contato`)
- **Layout**: `background: #262523`, `color: #E8E2D8`, `padding: clamp(64px, 10vh, 120px) clamp(20px, 5vw, 64px) 40px`. Grid `repeat(auto-fit, minmax(min(100%, 240px), 1fr))`, `gap: clamp(32px, 5vw, 72px)`, `max-width: 1320px`.
- **Coluna 1**: wordmark Marcellus 17px `letter-spacing: 0.26em` uppercase + linha 13.5px `rgba(232,226,216,0.6)`: "Tapeçaria e têxteis sob medida. Belo Horizonte, MG."
- **Coluna 2 "Contato"**: e-mail `contato@biapaduahome.com.br`, telefone `+55 31 3333 4444`, Instagram `@biapaduahome` — links 14.5px, hover `#C9A87C`. Sem formulário de orçamento.
- **Coluna 3 "Ateliê"**: "Visitas com agendamento prévio / Segunda a sexta, 9h às 18h", 14.5px `line-height: 1.8`.
- **Rodapé legal**: `border-top: 1px solid rgba(232,226,216,0.14)`, `padding-top: 22px`, 11px `letter-spacing: 0.14em` uppercase `rgba(232,226,216,0.35)`: "© 2026 Bia Pádua Home".
- **Labels de coluna**: 10.5px, `letter-spacing: 0.3em`, uppercase, `rgba(232,226,216,0.45)`.

## Interactions & Behavior
- **Abrir galeria**: clique em qualquer card de projeto (delegação de evento no container do grid via `closest('[data-project]')`). Recomenda-se, na implementação real, tornar o card um elemento focável (`<button>`/`<a>`) e trocar o overlay por rota (`/projetos/[slug]`) ou por um dialog acessível (`<dialog>` / focus trap + `aria-modal`).
- **Fechar galeria**: botão "Fechar" ou tecla `Escape`. Ao fechar, o scroll do body é restaurado.
- **Hover das imagens**: `transform: scale(1.035)`, 900ms `cubic-bezier(0.16,1,0.3,1)`.
- **Hover de links/nav**: opacidade ou cor de accent, sem sublinhado.
- **Fade-in ao rolar**: elementos `[data-reveal]` (6 cards + as 2 colunas do Sobre) entram com `opacity 0 → 1` e `translateY(22px) → 0`, `transition 1100ms cubic-bezier(0.16,1,0.3,1)`, stagger de `(index % 3) * 90ms`. Disparo por posição no scroll/resize quando `rect.top < innerHeight * 0.92`, checagem imediata no mount e fallback que revela tudo após 2,5s. **Importante**: no protótipo o IntersectionObserver não dispara no iframe de preview, daí a abordagem por scroll. Em produção, IO é aceitável, mas mantenha o fallback e respeite `prefers-reduced-motion` (revelar sem animação).
- **Responsivo (mobile-first)**: todo o espaçamento e a tipografia usam `clamp()`; os grids usam `auto-fit` + `minmax(min(100%, X), 1fr)`, então colapsam para 1 coluna sem media query. Os cards `span 2` continuam full-width. A nav de 3 itens não precisa de menu hambúrguer. Hero usa `100svh` (evita salto da barra do navegador em iOS).

## State Management
Estado mínimo, local:
- `active: string | null` — slug do projeto aberto na galeria (`serra`, `lourdes`, `belvedere`, `alphaville`, `savassi`, `vale`). `null` = overlay fechado.
- Efeitos colaterais: `body.style.overflow = 'hidden'` quando aberto; listener de `keydown` (Escape); listeners de `scroll`/`resize` do reveal, removidos quando todos os elementos já apareceram.
- Sem data fetching. Os projetos são um objeto estático (`PROJECTS`) com `title`, `meta`, `photos[]` — na implementação real, mover para CMS/JSON e derivar as rotas dele.
- Props/variantes do protótipo (opcionais no código final): mostrar/ocultar o ano nos cards, posição do texto do hero (inferior-esquerdo | centro), fade-in ligado/desligado.

## Design Tokens
**Cores**
- Charcoal (texto/fundo escuro): `#262523`
- Texto secundário escuro: `#4A463F`
- Cinza morno (parágrafo em fundo claro): `#6E6A63`
- Cinza têxtil (labels): `#8C877E`
- Cinza claro (ano/legenda): `#A8A29A`
- Areia clara (eyebrow do Sobre): `#A0968A`
- Branco creme (fundo base): `#F7F4EF`
- Creme escurecido (fundo do Sobre): `#F0EBE3`
- Placeholder de imagem: `#EDE7DE` / `#E3DCD2`
- Linhas: `#E3DCD2`, `#DFD7CB`, `#D7CFC3`
- Dourado/accent (hover em fundo escuro e links): `#B08D63` (claro: `#C9A87C`)
- Seleção de texto: `#E3D8C8`
- Texto sobre escuro: `#E8E2D8` (+ alfas 0.8 / 0.6 / 0.45 / 0.35 / 0.14)

**Tipografia** (Google Fonts)
- Display/títulos: `Marcellus`, 400 apenas.
- Texto/UI: `Jost`, 300–500.
- Escala: H1 `clamp(30px, 5.4vw, 62px)` / H2 `clamp(24px, 3.6vw, 42px)` / H3 card `clamp(18px, 1.6vw, 23px)` / corpo 15.5px / secundário 13.5px / meta 12.5px / label 11–11.5px / eyebrow 10.5px.
- Letter-spacing: wordmark 0.26em · eyebrow 0.30–0.34em · nav 0.22em · label 0.16–0.20em · legal 0.14em.
- Line-height: H1 1.12 · H2 1.20 · corpo 1.85 · secundário 1.6–1.8.

**Espaçamento** — padding de seção `clamp(72px, 12vh, 150px)` (vertical) / `clamp(20px, 5vw, 64px)` (horizontal, também usado pelo header e footer); gaps de grid `clamp(20px, 3vw, 40px)` a `clamp(40px, 6vw, 90px)`; stack interno 10 / 16 / 22 / 26px.

**Raio / sombra** — nenhum. Cantos retos (`border-radius: 0`) e zero box-shadow em toda a página; separação por linha de 1px e por whitespace.

**Larguras** — conteúdo `max-width: 1320px` (galeria 1500px); medida de texto 26ch–46ch.

**Easing** — `cubic-bezier(0.16, 1, 0.3, 1)` para reveal (1100ms) e hover de imagem (900ms); `ease` 300ms para botões.

## Assets
- **Nenhuma imagem final foi entregue.** Todos os 6 covers, o hero, a imagem do Sobre e as 24 fotos de galeria (6 projetos × 4) são placeholders. Os `placeholder="…"` de cada slot no HTML descrevem o conteúdo pretendido de cada foto — use-os como briefing de fotografia.
- Formatos recomendados: AVIF/WebP com fallback JPEG; hero ~2400px na maior dimensão; covers ~1600px; galeria ~1800px. `srcset` por breakpoint, `loading="lazy"` fora do hero.
- Fontes: Marcellus e Jost via Google Fonts (ou self-hosted com `@font-face` + `font-display: swap`).
- Ícones: nenhum. Logo: wordmark tipográfico, sem arquivo de marca.

## Files
- `Bia Padua Home.dc.html` — o design completo (markup + lógica). Referência principal.
- `image-slot.js` — componente de placeholder de imagem usado apenas no protótipo. **Não portar**: substituir por imagens reais.
