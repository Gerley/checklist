## 2. Publicando o Projeto em uma Pagina GitHub

Neste tutorial, iremos publicar o nosso checklist em uma pagina GitHub.

Ele é baseado no [artigo](https://vuejs-brasil.com.br/exporte-seu-projeto-vue-para-o-github-pages/)

### 2.1 Criando o Repositorio no GitHub

Crio o Repositorio **checklist** no GitHub.


https://medium.com/@shaibenshimol/build-todo-list-with-vuejs-vuex-vuetify-and-firebase-9eeed476e596



https://codelabs.developers.google.com/codelabs/your-first-pwapp/?hl=pt-br#4

https://cli.vuejs.org/core-plugins/pwa.html

https://medium.com/@n11sh1/how-to-build-pwa-w-vue-cli-3-service-workers-add-to-home-screen-push-notifications-b519c49e142d

## 1. Crie um Projeto Vuetify
Criando um projeto Vuetify com pwa.

```sh
vue create my-app
cd my-app
vue add vuetify
vue add pwa
```

## 2. Adicionando o Manifest.json
Crie o arquivo manifest.json na pasta public.
```json
{
    "name": "minha-casa",
    "short_name": "minha-casa",
    "icons": [
        {
            "src": "/img/icons/icon-128x128.png",
            "sizes": "128x128",
            "type": "image/png"
        },
        {
            "src": "/img/icons/icon-144x144.png",
            "sizes": "144x144",
            "type": "image/png"
        },
        {
            "src": "/img/icons/icon-152x152.png",
            "sizes": "152x152",
            "type": "image/png"
        },
        {
            "src": "/img/icons/icon-192x192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "/img/icons/icon-256x256.png",
            "sizes": "256x256",
            "type": "image/png"
        },
        {
            "src": "/img/icons/icon-512x512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ],
    "start_url": "/index.html",
    "display": "standalone",
    "background_color": "#3E4EB8",
    "theme_color": "#2F3BA2"
}
```
E adicione o comando abaixo no arquivo **index.html**:
```html
<link rel="manifest" href="/manifest.json">
```

## Adicionando uma meta tags IOS 

Adicione o codigo abaixo no  arquivo **index.html**.
```html
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<meta name="apple-mobile-web-app-title" content="Weather PWA">
<link rel="apple-touch-icon" href="/images/icons/icon-152x152.png">
```

## Adicionando uma meta descricao

Adicione o codigo abaixo no arquivo **index.html**.
```html
<meta name="description" content="A sample weather app">
```

## Adicionando um cor na barra de endereco
Adicione o codigo abaixo no arquivo **index.html**.
```html
<meta name="theme-color" content="#2F3BA2" />
```

## Adicine ao arquivo vue.config.js
publicPath: process.env.NODE_ENV === 'production'
    ? '/minha-casa/'
    : '/'
