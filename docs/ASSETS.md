# Recursos visuais

Identidade visual da Calculadora RTC: azul-marinho `#12304a`, teal `#087f8c`, verde `#71d9bf`, dourado `#e9b95c` e fundo claro `#f5f8fa`.

## Arquivos e integração

- `images/logo/logo.svg`: logotipo horizontal para desktop, configurado em `_config.yml`.
- `images/logo/logo-mobile.svg`: símbolo compacto para o cabeçalho móvel.
- `images/favicon.svg` e `images/favicon-32x32.svg`: símbolo vetorial; o segundo preserva o caminho esperado pelo tema Serif.
- `favicon.ico`: tamanhos 16, 32 e 48 px. PNGs de 16, 32, 180, 192 e 512 px em `images/` atendem navegadores, Apple e Android.
- `site.webmanifest`: ícones com caminhos relativos ao projeto, inclusive no GitHub Pages.
- `images/illustrations/rtc-calculo.webp` e `rtc-componentes.webp`: ilustrações principais, 1536 × 1024 px, com variantes `-768.webp` de 768 × 512 px e fallback JPEG progressivo. A ilustração de cálculo também é usada no compartilhamento social.
- `images/illustrations/tributos-rtc.svg` e `tributos-rtc-mobile.svg`: cartões vetoriais de IBS, CBS e IS, com disposição horizontal ou vertical e textos acessíveis.
- `images/social/`: ícones vetoriais de repositório, email e website. `_data/social.json` usa os contatos reais do projeto em lugar das redes de demonstração do tema.
- `assets/css/rtc-visuals.css`: apresentação responsiva e movimento discreto ao passar o mouse, respeitando a preferência de movimento reduzido.
- `_includes/rtc-head.html`: declarações de favicon e manifesto, incluídas por `_layouts/default.html`.

As ilustrações foram geradas com a ferramenta integrada **image_gen**, sem API ou CLI de geração. Os SVGs do logotipo, favicon e cartões foram desenhados diretamente como vetores. A conversão para WebP/JPEG e o redimensionamento preservam a composição das imagens geradas. Os arquivos originais gerados permanecem no diretório padrão da ferramenta; todas as versões consumidas pelo site estão neste projeto.

As imagens são conceituais; não representam a interface real da aplicação. A identidade visual é própria do projeto e não utiliza símbolos oficiais da Receita Federal.

## Prompts finais

### Ilustração de abertura

```text
Use case: stylized-concept
Asset type: wide hero illustration for the Calculadora RTC documentation website, a Brazilian open source consumption tax calculator.
Primary request: an elegant editorial 3D still life about precise digital tax calculation. A deep navy calculator with mint green keys, three simple translucent teal and blue geometric pillars, a white document with minimal abstract lines, and a few connected data nodes, arranged as one balanced scene. This is conceptual art, not an app interface.
Scene/backdrop: very light cool ivory background, subtle pale blue floor and soft ambient shadows.
Style/medium: sophisticated minimal clay and frosted glass 3D editorial illustration, clean rounded edges, fine rendering, professional and approachable.
Composition/framing: wide landscape 3:2 composition; objects comfortably spaced with generous clean margins; focal group centered, no cropped objects, no framing border.
Color palette: midnight navy #12304a, teal #087f8c, mint #71d9bf, tiny warm gold #e9b95c highlights, ivory #f5f8fa.
Text: none. Calculator display blank or simple abstract horizontal bars.
Constraints: no words, no letters, no percentages, no tax rates, no maps, no logos, no national or government emblems, no watermark; no extra visual clutter.
```

### Integração dos componentes

```text
Use case: stylized-concept
Asset type: editorial supporting illustration for the Components section of the Calculadora RTC open source documentation website.
Primary request: represent a web frontend connected to a calculation backend. A minimal floating ivory browser window with simple blue and mint abstract UI blocks on the left, a neat stack of three navy server modules on the right, connected by one elegant curved teal conduit with small mint nodes. One small abstract calculator tile between the components.
Scene/backdrop: pale cool ivory studio floor and background with soft contact shadows.
Style/medium: sophisticated rounded clay and frosted glass 3D editorial rendering, professional and approachable, matching a navy calculator with mint keys illustration.
Composition/framing: wide landscape 3:2, comfortable clean margins, balanced single scene, no cropped objects.
Color palette: midnight navy #12304a, teal #087f8c, mint #71d9bf, small warm gold #e9b95c details, ivory #f5f8fa.
Text: none.
Constraints: illustrative concept only, no readable code, no words or letters, no logos, no watermark, no national or government emblems, no unnecessary objects.
```

## Manutenção

Os caminhos HTML usam `relative_url`; a imagem social usa `absolute_url`. As imagens fora da abertura usam carregamento tardio. Os tamanhos intrínsecos estão declarados para evitar deslocamento do conteúdo durante o carregamento.

O layout `_layouts/default.html` adapta o layout do [Jekyll Serif](https://github.com/zerostaticthemes/jekyll-serif-theme), mantendo seus includes e sua folha de estilos. Esse arquivo local prevalece sobre futuras atualizações do layout remoto; revisar a integração ao trocar o tema.

