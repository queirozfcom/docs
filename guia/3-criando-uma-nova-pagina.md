# Criando uma página

Abra o arquivo `storefront/components/HomePage.json`. Esse arquivo fala para o servidor as seguintes informações:

- **route**: O componente de sua app com nome "HomePage" (neste caso "alphateam.my-first-app") irá atender o path `/` e será identificado no código como "home".

- **assets**: Para que essa página funcione, os arquivos listados nessa propriedade devem estar inseridas na página e o servidor se encarregará de inserir os arquivos no HTML quando o usuário entrar na página.

### Gerando os arquivos de uma nova página

Vamos usar novamente o generator: dessa vez, para gerar os arquivos necessários para se criar uma nova página.

Abra o terminal na pasta do seu projeto e digite:
```
yo vtex:component
```
E responda as perguntas com:
- "Page"
- "ProductPage"
- "product"
- "/:slug/p"
- "y"

O generator acabou de criar os arquivos abaixo e alterou o `webpack.config.js`.

- `src/pages/ProductPage/ProductPage.js`
- `src/pages/ProductPage/index.js`
- `storefront/components/ProductPage.json`

Para ver o componente gerado, entre na URL:

[http://sualoja.local.myvtex.com:3000/short-balneario/p](http://sualoja.local.myvtex.com:3000/short-balneario/p)

Você deve ver um texto na tela:
> My new component ProductPage!

Está tudo funcionando! Agora, vamos explicar o que cada um destes arquivos gerados faz.

### Arquivo de definição do componente

O arquivo gerado na pasta `storefront/components`, `ProductPage.json`, define informações importantes para o servidor. Ele tem o seguinte conteúdo:

```json
{
  "route": {
    "name": "product",
    "path": "/:slug/p"
  },
  "assets": [
    "common.js",
    "ProductPage.js"
  ]
}
```

Estamos criando uma página chamada "product", que será aberta quando o usuário digitar algo como "/short-balneario/p". Observe a notação ":slug", significa que esse valor é variável.

A propriedade `assets` indica quais os arquivos necessários para a página. O Webpack gera arquivos separados para cada página (por ex: `HomePage.js` e `ProductPage.js`) e um arquivo que possui os módulos comum a todas elas (`common.js`).


### O componente React da página

O arquivo `src/pages/ProductPage/ProductPage.js` é o componente React que responde pela rota de produto.

```js
import React from 'react';

class ProductPage extends React.Component {
  render() {
    return (
      <h1>My new component ProductPage!</h1>
    );
  }
}

export default ProductPage;

```

### O arquivo principal da página

O arquivo `src/pages/ProductPage/index.js` é o arquivo principal da página. O seu código Javascript começa nesse arquivo.

```js
// Importa as actions do SDK
import { actions } from 'sdk';
// Importa o componente React
import ProductPage from './ProductPage';

let components = [
  {
    name: 'ProductPage@alphateam.my-first-app',
    constructor: ProductPage
  }
];

// Chama a action que registra os componentes
actions.ComponentActions.register(components);

// Não preste atenção nisso, é algo que temos que colocar para o hot loader funcionar
// Enable react hot loading with external React
// see https://github.com/gaearon/react-hot-loader/tree/master/docs#usage-with-external-react
if (module.hot) {
  window.RootInstanceProvider = require('react-hot-loader/Injection').RootInstanceProvider;
}

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
    name: 'ProductPage@alphateam.my-first-app',
    constructor: ProductPage
  }
];

// Chama a action que registra os componentes
actions.ComponentActions.register(components);
```

Estamos chamando a *action* `register` da `ComponentActions`. Essa *action* faz com que os componentes sejam registrados na `ComponentStore`. Ao registrar os componentes, o Storefront SDK consegue pegar o componente na *store* e, quando a rota do componente é aberta, ele renderiza o componente associado.

Atualize a página do browser para ver as modificações (o hot loader funciona apenas para alterações em componentes React). Você deve agora ver a página de produto!

## Recapitulando

Para criar uma nova página você precisa:

- Criar um arquivo JSON com o nome do componente React que irá responder pela rota em `storefront/components/`
- Criar um componente React em `src/pages/`
- Registrar o componente React utilizando a *action* `ComponentActions.register`

---

Você completou o "Criando uma nova página"! Você já sabe como criar uma página e registrar componentes.

Próximo passo: [Pegando dados do servidor](4-pegando-dados-do-servidor.md)
