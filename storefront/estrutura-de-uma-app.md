# Estrutura de uma app

Uma app no Storefront é estruturada da seguinte maneira:

```
.
├── storefront/
│   ├── assets/
│   ├── components/
│   ├── models/
│   └── layout.html
└── meta.json
```

## Assets

Nessa pasta estão todos os arquivos estáticos necessários para a app. Isso inclui: arquivos Javascript, CSS, imagens, fontes, etc.

## Components

Nessa pasta moram arquivos de definição de componentes que respondem por uma rota.

Exemplo de um arquivo chamado `ProductPage.json`:
```json
{
  "route": {
    "name": "product",
    "path": "/:product/p"
  },
  "model": {
    "name": "product@vtex.storefront-sdk",
    "params": {
      "product": "{{ route.params.product }}"
    }
  },
  "assets": [
    "storefront-theme.js"
  ]
}
```

A rota deve sempre conter `name` e `path`, seguindo os moldes do [React Router](http://rackt.github.io/react-router/), componente React usado internamente para roteamento da aplicação.

O parâmetro `model` define `models` que devem ser carregados no lado do servidor. Muitas vezes esse modelo precisa de um parâmetro da rota, como mostrado no exemplo. Você deverá usar `models` sempre que quiser que os dados carregados possam ser lidos pelo Google.

Por fim, o parãmetro `assets` define quais arquivos dentro da pasta `assets` são necessários para renderizar essa página.

## Models

Models definem a configuração de um dado que deve ser requisitado pelo servidor. Ele pode receber alguns parâmetros definidos pela rota.

Os dados dessa chamada ficam disponíveis na variável global na página chamada `window.storefront`.

Exemplo de um arquivo chamado `product.json`:
```json
{
  "url": "http://api.beta.vtex.com/:account/products/:product",
  "cacheDuration": 60,
  "parameters": {
    "account": "{{ account.name }}"
  },
  "queryString": {
    "query": "{{ parameters.query }}"
  }
}
```

## `layout.html`

Esse arquivo é necessário apenas caso seja uma app de tema. Ele define o HTML base de sua loja.
