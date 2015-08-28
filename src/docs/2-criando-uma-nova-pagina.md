# Criando uma página

Abra o arquivo `storefront/components/HomePage.json`. Esse arquivo fala para o servidor as seguintes informações:

- **route**: O componente com nome "HomePage" da sua app (nesse caso "alphateam.my-first-app") irá atender o path `/` e ela será identificada no código como "home"
- **assets**: Para que essa página funcione, os arquivos listados nessa propriedade devem estar inseridas na página, e o servidor se encarregará de inserir os arquivos no HTML quando o usuário entrar nessa página

Vamos agora criar um novo arquivo na pasta `storefront/components`, dê o nome de "ProductPage.json" e coloque o seguinte JSON:

```json
{
  "route": {
    "name": "product",
    "path": "/:slug/p"
  },
  "assets": [
    "my-first-app.js"
  ]
}
```

Estamos criando uma página chamada "product", que será aberta quando o usuário digitar algo como "/short-balneario/p". Note a notação ":slug", significa que esse valor é variável.

A propriedade `assets` usa o mesmo arquivo que a "HomePage" pois o Webpack faz o build de toda a aplicação em um único arquivo.

Entre na URL:

[http://basedevmkp.local.myvtex.com:3000/short-balneario/p](http://basedevmkp.local.myvtex.com:3000/short-balneario/p)

Veja que a página está em branco. Isso acontece pois ainda não escrevemos um componente React para atender a essa rota — vamos criá-lo agora.

Crie o arquivo `ProductPage.jsx` na pasta `src/pages/` com o seguinte código:

```js
import React from 'react';

class ProductPage extends React.Component {
  render() {
    return (
      <h1>Essa é a página de produto!</h1>
    );
  }
}

export default ProductPage;

```

Nada deve acontecer. Isso acontece, pois nosso arquivo principal `src/my-first-app.jsx` não está importando o componente "ProductPage". Abra o arquivo `src/my-first-app.jsx` e substitua o conteúdo pelo seguinte código:

```js
// Importa componentes que respondem por uma página
import HomePage from 'pages/HomePage';
import ProductPage from 'pages/ProductPage';
// Importa dispatcher do SDK
import { dispatcher } from 'sdk';

let components = [
  {
    name: 'HomePage@vtex.my-first-app',
    constructor: HomePage
  },
  {
    name: 'ProductPage@vtex.my-first-app',
    constructor: ProductPage
  }
];

// Chama a action que registra os componentes
dispatcher.actions.ComponentActions.register(components);

// Não preste atenção nisso, é algo que temos que colocar para o hot loader funcionar
// Enable react hot loading with external React
// see https://github.com/gaearon/react-hot-loader/tree/master/docs#usage-with-external-react
if (module.hot) {
  window.RootInstanceProvider = require('react-hot-loader/Injection').RootInstanceProvider;
}

```

```js
// Importa componentes que respondem por uma página
import HomePage from 'pages/HomePage';
import ProductPage from 'pages/ProductPage';
```

Primeiro, importamos os componentes de página usando a sintaxe da versão ES6 do Javascript. O componente é importado de "pages/ProductPage" e seu construtor é inserido na variável `ProductPage`.

```js
// Importa o dispatcher do SDK
import { dispatcher } from 'sdk';
```

Depois pegamos apenas a variável `dispatcher` da biblioteca SDK. Essa variável guarda o *dispatcher*, um objeto conceituado pelo [Flux](https://facebook.github.io/flux/docs/overview.html#structure-and-data-flow).

---

## Uma rápida explicação sobre Flux em 30 segundos

O Flux é uma arquitetura que define como os dados são transmitidos por toda a aplicação.

![Flux](https://facebook.github.io/flux/img/flux-simple-f8-diagram-with-client-action-1300w.png)

A View representa os componentes React. O dispatcher é a unidade centralizadora: ele liga as actions às stores. As stores são onde os dados estão armazenados, e os componentes podem ouvir mudanças de uma store. As actions fornecem funções que os componentes podem chamar, fazendo com que os dados das stores mudem. Atenção: as funções das actions não retornam resultados, elas apenas fazem com que as stores mudem e, como os componentes escutam as mudanças das stores, os componentes pegam esses novos dados.

---

```js
let components = [
  {
    name: 'HomePage@vtex.my-first-app',
    constructor: HomePage
  },
  {
    name: 'ProductPage@vtex.my-first-app',
    constructor: ProductPage
  }
];

// Chama a action que registra os componentes
dispatcher.actions.ComponentActions.register(components);
```

Estamos chamando a action `register` da "ComponentActions". Essa action faz com que os componentes sejam registrados na "ComponentStore". Ao registrar os componentes, o SDK consegue pegar o componente na store e, quando a rota do componente é aberta, ele renderiza o componente associado.

Atualize a página do browser para ver as modificações (o hot loader funciona apenas para alterações em componentes React). Você deve agora ver a página de produto!

## Recapitulando

Para criar uma nova página você precisa:

- Criar um arquivo JSON com o nome do componente React que irá responder pela rota em `storefront/components/`
- Criar um componente React em `src/pages/`
- Registrar o componente React utilizando a action "ComponentActions.register"

---

Você completou o "Criando uma nova página"! Você já sabe como criar uma página e registrar componentes.

Próximo passo: [Pegando dados do servidor](3-pegando-dados-do-servidor.md)
