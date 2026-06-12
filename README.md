# Portfolio - Paulo Roberto Sousa Pereira

Site estatico (HTML/CSS/JS, sem build) servido pelo nginx.

## Estrutura

```
portfolio/
├── index.html
└── assets/
    ├── css/styles.css
    ├── js/main.js
    └── img/            screenshots dos projetos
```

## Rodar localmente

Abra `index.html` no navegador, ou suba um servidor simples:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Adicionar um novo projeto

No `index.html`, copie um bloco `<li class="card"> ... </li>` e ajuste:

- `data-accent`: `amber`, `teal` ou `slate` (cor do thumbnail)
- numero em `card__index`, titulo, descricao, tags
- `href` do link para o projeto no ar

## Usar screenshot real no card (opcional)

Os cards usam um gradiente com monograma por padrao. Para usar uma imagem:

1. Coloque o arquivo em `assets/img/` (ex: `chopp.png`).
2. Adicione um `style` inline no `.card__thumb` daquele card:

```html
<div class="card__thumb" style="background-image:url('assets/img/chopp.png')">
```

A imagem cobre o thumb automaticamente; pode remover o `<span class="card__monogram">`.

## Cache: atualizar CSS/JS (obrigatorio)

O nginx serve os assets com cache agressivo (`Cache-Control: immutable`,
`expires 1y`) e os nomes dos arquivos nao tem hash. O navegador so rebaixa
um arquivo se a URL mudar. Por isso, sempre que editar
`assets/css/styles.css` ou `assets/js/main.js`, incremente o `?v=N` da
respectiva tag no `index.html`:

```html
<link rel="stylesheet" href="assets/css/styles.css?v=1" />  <!-- ?v=2, ?v=3 ... -->
<script src="assets/js/main.js?v=1" defer></script>
```

Incremente cada arquivo de forma independente (so o que foi alterado). Se
esquecer, os visitantes ficam com a versao antiga por ate um ano.

