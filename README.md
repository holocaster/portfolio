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

## Publicar no VPS (nginx)

1. Copie a pasta para o servidor:

```bash
rsync -av --delete ./ usuario@SEU_VPS:/var/www/portfolio/
```

2. Bloco de server no nginx (ex: `/etc/nginx/sites-available/portfolio`):

```nginx
server {
    listen 80;
    server_name SEU_DOMINIO;   # ex: portfolio.prsites.com.br

    root /var/www/portfolio;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # cache de assets estaticos
    location ~* \.(css|js|png|jpg|jpeg|svg|woff2)$ {
        expires 30d;
        add_header Cache-Control "public";
    }
}
```

3. Ative e recarregue:

```bash
sudo ln -s /etc/nginx/sites-available/portfolio /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
```

4. HTTPS gratis com certbot:

```bash
sudo certbot --nginx -d SEU_DOMINIO
```
