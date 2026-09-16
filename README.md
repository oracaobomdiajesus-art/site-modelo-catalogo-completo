# Site Modelo Catálogo Completo

Template de site institucional "completo" (várias seções, estilo site profissional) + catálogo de produtos com carrinho, feito em [Hugo](https://gohugo.io/), pronto para publicar grátis no Cloudflare (Workers com arquivos estáticos) e editar pelo [Pages CMS](https://pagescms.org/).

É o `site-modelo-institucional-completo` com uma página de catálogo de verdade a mais: produtos por categoria, busca, carrinho (salvo no navegador do cliente) e checkout via WhatsApp ou Pix. Sem painel administrativo próprio, sem integração com planilha e sem pagamento online — o pedido final é sempre combinado direto com o cliente pelo WhatsApp.

## Seções da página inicial

1. **Cabeçalho fixo** — logo, nome, menu com âncoras, botão de WhatsApp
2. **Hero** — selo, título com destaque colorido, descrição, dois botões, foto
3. **Quem Somos** — fotos, texto e 3+ selos de credibilidade (lista editável)
4. **Serviços** — grade de cards (ícone, título, descrição, botão opcional) — quantos você quiser
5. **Produtos** *(opcional, liga/desliga)* — mostra os produtos marcados como "Destaque" e um botão "Ver Catálogo Completo"
6. **Faixa de aviso** *(opcional, liga/desliga)* — texto rolante
7. **Blog/Notícias** *(opcional, liga/desliga)* — só aparece se tiver post publicado
8. **Localização** — mapa do Google incorporado (gerado a partir do endereço, sem precisar de chave de API) + botão "Como Chegar"
9. **Rodapé** — logo, links rápidos, contato, redes sociais, copyright automático
10. **Botão flutuante de WhatsApp**

## Página de Catálogo (`/produtos/`)

Grade completa de produtos organizados por categoria, com abas de categoria, busca por nome/descrição/código, carrinho lateral e dois jeitos de fechar o pedido:
- **Enviar pedido pelo WhatsApp** — abre uma conversa já com a lista de itens e o total
- **Já paguei via Pix — enviar pedido** — só aparece se a chave Pix estiver preenchida no perfil

## Como usar este template para um novo cliente

1. Crie um novo repositório a partir deste
2. No Cloudflare, crie um projeto do tipo **Worker** conectado ao repositório:
   - **Comando da build**: `hugo --minify`
   - **Comando de implantação**: `npx wrangler deploy`
   - **Diretório raiz**: `/`
3. Configure o [Pages CMS](https://pagescms.org/) apontando pro repositório — o `.pages.yml` já define todos os campos
4. Edite `content/_index.md` e as coleções (`selos`, `servicos`, `categorias`, `produtos`, `blog`) com as informações reais do cliente
5. Ligue "Produtos" e/ou "Blog" no perfil só se o cliente for usar essas seções

## Estrutura

```
content/
  _index.md    → perfil + textos de todas as seções fixas
  selos/       → selos de credibilidade (Quem Somos)
  servicos/    → cards de serviços
  categorias/  → categorias do catálogo
  produtos/    → produtos do catálogo (com preço, foto, estoque, promoção)
  blog/        → posts do blog/notícias (seção opcional)
layouts/
  index.html            → monta a página inicial, seção por seção
  produtos/list.html     → página do catálogo completo
  blog/list.html         → lista de posts
  blog/single.html        → post individual
  partials/
    header.html, footer.html, theme-style.html, analytics.html
    product-card.html, cart-panel.html
static/
  css/style.css   → todo o visual do site
  js/main.js      → menu mobile
  js/cart.js      → lógica do carrinho (localStorage) e checkout
  js/catalogo.js  → busca e filtro de categorias no catálogo
  img/            → logo, fotos, fundo, produtos
```

## Desenvolvimento local

Requer [Hugo](https://gohugo.io/installation/) instalado.

```
hugo server -D
```
