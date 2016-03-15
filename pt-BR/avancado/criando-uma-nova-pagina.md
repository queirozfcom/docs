# Criando uma página

Este guia tem como objetivo a criação de um novo modelo de página no Storefront que responda a uma rota — por exemplo, uma página de categoria ou de busca.

Para começar, vamos dar uma olhada no arquivo `storefront/routes/home.json`. Esse arquivo fala para o servidor as seguintes informações:

- **path**: Definimos uma rota para o path `/` e será identificado no código como "home" (nome do arquivo).

Agora, vejamos o arquivo `storefront/components/HomePage.json`. Esse arquivo fala para o servidor as seguintes informações:

- **assets**: Para que essa página funcione, os arquivos listados nessa propriedade devem estar inseridas na página e o servidor se encarregará de inserir os arquivos no HTML quando o usuário entrar na página.

Por fim, vamos inspecionar o arquivo `storefront/settings/routes/home/Root@vtex.storefront-sdk/content.json`. 
O componente Root é o ponto de entrada para o carregamento de componentes de qualquer rota, toda rota precisa ter um Root configurado.

Esse arquivo fala para o servidor as seguintes informações:

- **component**: Definimos o componente responsável por atender ao conteúdo do Root. Neste caso, o componente ProductPage.

### Gerando os arquivos de uma nova página

Vamos usar novamente o [vtex generator](../introducao/ecossistema.md): dessa vez, para gerar os arquivos necessários para se criar uma nova página.

Abra o terminal na pasta do seu projeto e digite:
```
yo vtex:component
```
E responda as perguntas com:
- `Page`
- `ProductPage`
- `product`
- `/:slug/p`
- `y`

O generator acabou de criar os arquivos abaixo e alterou o `webpack.config.js`.

- `src/components/ProductPage/ProductPage.js`
- `src/components/ProductPage/index.js`
- `storefront/components/ProductPage.json`
- `storefront/settings/routes/product/Root@vtex.storefront-sdk/content.json`
- `storefront/routes/product.json`

Para ver o componente gerado, entre na URL:

[http://sualoja.local.myvtex.com:3000/moto-x/p](http://sualoja.local.myvtex.com:3000/moto-x/p)

Você deve ver um texto na tela:
> My new component ProductPage!

Está tudo funcionando! Agora, vamos explicar o que cada um destes arquivos gerados faz:

### Arquivo de definição do componente

Os arquivos gerados `storefront/routes/product.json`, `storefront/components/ProductPage.json`, `storefront/settings/routes/product/Root@vtex.storefront-sdk/content.json`, definem informações importantes para o servidor. Eles tem o seguinte conteúdo:

**routes/product.json**
```json
{
  "path": "/:slug/p"
}
```

**components/product.json**
```json
{
  "assets": [
    "common.js",
    "ProductPage.js"
  ]
}
```

**storefront/settings/routes/product/Root@vtex.storefront-sdk/content.json**
```json
{
  "component": "ProductPage@nome-da-sua-empresa.nome-da-sua-app"
}
```

Estamos criando uma página chamada "product", que será aberta quando o usuário digitar algo como "/moto-x/p". Observe a notação ":slug", significa que esse valor é variável.

A propriedade `assets` indica quais os arquivos necessários para a página. O Webpack gera arquivos separados para cada página (por ex: `HomePage.js` e `ProductPage.js`) e um arquivo que possui os módulos comum a todas elas (`common.js`).


### O componente React da página

O arquivo `src/components/ProductPage/ProductPage.js` é o componente React que responde pela rota de produto.

```js
import React from 'react';

class ProductPage extends React.Component {
  render() {
    return (
      <div>
        <h1>My new component ProductPage!</h1>
      </div>
    );
  }
}

export default ProductPage;
```

### O arquivo principal da página

O arquivo `src/components/ProductPage/index.js` é o arquivo principal da página. O seu código Javascript começa nesse arquivo.

```js
// Importa as actions do SDK
import { actions } from 'sdk';
// Importa o componente React
import ProductPage from './ProductPage';

let components = [
  {
    name: 'ProductPage@mycompany.my-first-app',
    constructor: ProductPage
  }
];

// Chama a action que registra os componentes
actions.ComponentActions.register(components);
```

```js
// Importa as actions do SDK
import { actions } from 'sdk';
// Importa o componente React
import ProductPage from './ProductPage';
```

Primeiro, importamos as `actions` do Storefront SDK e o componente React usando a sintaxe da versão ES6 do Javascript.

O componente é importado do arquivo em "./ProductPage" e seu construtor é inserido na variável `ProductPage`.

O Storefront SDK está disponível no contexto da página, por isso, não precisamos especificar o local do arquivo (como fizemos com `./ProductPage`), usamos apenas `'sdk'`. Dele nós pegamos apenas a variável `actions`. Essa variável guarda todas as *actions*, um objeto conceituado pelo [Flux](https://facebook.github.io/flux/docs/overview.html#structure-and-data-flow).

---

## Uma rápida explicação sobre Flux em 30 segundos

O Flux é uma arquitetura que define como os dados são transmitidos por toda a aplicação.

![Flux](https://facebook.github.io/flux/img/flux-simple-f8-diagram-with-client-action-1300w.png)

A *View* representa os componentes React. O *dispatcher* é a unidade centralizadora: ele liga as *actions* às *stores*. As *stores* são onde os dados estão armazenados, e os componentes podem ouvir mudanças de uma *store*. As *actions* fornecem funções que os componentes podem chamar, fazendo com que os dados das *stores* mudem. Atenção: as funções das *actions* não retornam resultados, elas apenas fazem com que as *stores* mudem e, como os componentes escutam as mudanças das *stores*, eles são renderizados novamente com os dados atualizados.

---

```js
let components = [
  {
    name: 'ProductPage@nome-do-seu-vendor.nome-da-sua-app',
    constructor: ProductPage
  }
];

// Chama a action que registra os componentes
actions.ComponentActions.register(components);
```

Estamos chamando a *action* `register` da `ComponentActions`. Essa *action* faz com que os componentes sejam registrados na `ComponentStore`. Ao registrar os componentes, o Storefront SDK consegue pegar o componente na *store* e, quando a rota do componente é aberta, ele renderiza o componente associado.

Atualize a página do browser para ver as modificações (o hot loader funciona apenas para alterações em componentes React). Você deve agora ver a página de produto!

---

## Recapitulando

Para criar uma nova página você precisa:

- Criar o arquivo JSON que define a rota em `storefront/routes/`
- Criar o arquivo JSON que define o componente em `storefront/components/`
- Criar o arquivo JSON que define qual componente responderá pela rota em `storefront/settings/routes/product/Root@vtex.storefront-sdk/content.json`
- Criar um componente React em `src/components/`
- Registrar o componente React utilizando a *action* `ComponentActions.register`

---


## Próximos Passos

Você completou o "Criando uma nova página"! Você já sabe como criar uma página e registrar componentes. Agora vamos aprender como [criar um editor](/criando-um-editor.md).
