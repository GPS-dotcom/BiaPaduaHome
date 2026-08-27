# Site pronto para publicar — Bia Pádua Home

`site/index.html` é o site completo em HTML/CSS/JS puro, sem build e sem dependências.
Abrir no navegador já funciona. É o caminho mais curto: o Claude Code só precisa
colocar as fotos e publicar.

## O que falta
Apenas as imagens. O HTML espera esta estrutura dentro de `site/`:

```
site/
  index.html
  images/
    hero.jpg              ambiente decorado, horizontal, luz natural (~2400px)
    sobre.jpg             retrato da Bia ou detalhe de tecido/ateliê, vertical 3:4
    serra/cover.jpg       capa do projeto (16:10)   + 1.jpg 2.jpg 3.jpg 4.jpg (3:2)
    lourdes/cover.jpg     capa (4:5)                + 1.jpg 2.jpg 3.jpg 4.jpg
    belvedere/cover.jpg   capa (4:5)                + 1.jpg 2.jpg 3.jpg 4.jpg
    alphaville/cover.jpg  capa (16:10)              + 1.jpg 2.jpg 3.jpg 4.jpg
    savassi/cover.jpg     capa (4:5)                + 1.jpg 2.jpg 3.jpg 4.jpg
    vale/cover.jpg        capa (4:5)                + 1.jpg 2.jpg 3.jpg 4.jpg
```

As legendas de cada foto estão no array `PROJECTS`, no fim do `index.html` — elas
descrevem o que cada imagem deve mostrar. Enquanto uma foto não existir, o espaço
aparece em bege (`#EDE7DE`), sem quebrar o layout.

## Onde editar
Todo o conteúdo dos projetos vive em um único array `PROJECTS` no fim do arquivo:
slug, título, categorias, ano, cidade e as 4 legendas. Adicionar um projeto = um
objeto novo no array + a pasta de imagens correspondente. `wide: true` faz o card
ocupar duas colunas no grid.

Contato (e-mail, telefone, Instagram) está no `<footer>`; o Instagram aponta para
`instagram.com/biapaduahome` — confirmar o handle real.

## Publicar
Qualquer host estático serve. Não há backend.

- **Netlify / Cloudflare Pages / Vercel**: arrastar a pasta `site/` na interface, ou
  conectar o repositório com build command vazio e publish directory `site`.
- **GitHub Pages**: commitar o conteúdo de `site/` na branch `gh-pages` (ou em `/docs`).
- **Servidor próprio**: copiar `site/` para o document root.

Teste local: `npx serve site` (ou abrir o arquivo direto).

## Tarefas recomendadas para o Claude Code
1. Colocar as fotos em `images/` seguindo a árvore acima.
2. Gerar versões WebP/AVIF e trocar cada `<img>` por `<picture>` com `srcset`
   (mantendo o JPEG como fallback) — é o único ganho real de performance que falta.
3. Conferir os dados de contato e o handle do Instagram.
4. Adicionar favicon e uma imagem `og:image` para compartilhamento.
5. Publicar em um host estático e apontar o domínio.

Não há framework a escolher, nem porte a fazer. Caso no futuro o site cresça
(blog, muitos projetos, CMS), o `README.md` na pasta acima documenta todos os
tokens e comportamentos para uma reimplementação em Next.js ou Astro.
