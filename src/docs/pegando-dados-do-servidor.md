# Pegando dados do servidor

Temos duas páginas: a home e a página de produto.

> Mas o que é uma pagina de produto sem produtos?

Vamos aprender a pegar dados da API pra preencher essa página.

Copie o JSON e coloque no arquivo `storefront/components/ProductPage.json`:

```json
{
  "route": {
    "name": "product",
    "path": "/:slug/p"
  },
  "resourceBinding": {
    "locator": "product@vtex.storefront-sdk",
    "params": {
      "slug": "{{ route.slug }}"
    }
  },
  "assets": [
    "my-first-app.js"
  ]
}
```

Veja que inserimos uma nova propriedade chamada `resourceBinding`. Os parâmetros que ele recebe são:

- **locator**: identificador do resource que será usado. Neste caso estamos usando um resource do SDK chamado "product", responsável por pegar um produto da API
- **params**: são os parâmetros necessários para o resource. O resource "product" precisa do parâmetro "slug", pegamos esse dado fornecido pela rota

O `resourceBinding` liga uma rota a uma chamada a API.

Carregue a página de produto no browser ([http://basedevmkp.local.myvtex.com:3000/short-balneario/p](http://basedevmkp.local.myvtex.com:3000/short-balneario/p)), clique com o botão direito do mouse e veja o código fonte. Você pode ver que os dados do produto estão impressos na página. O SDK pega esses dados automaticamente e os insere dentro da store "ProductStore".

Vamos fazer com que o nosso código React acesse essa store e imprima o nome do produto na página.

Copie o seguinte código e coloque no arquivo `src/pages/ProductPage.jsx`:
```js
import React from 'react';
import { dispatcher } from 'sdk';

class ProductPage extends React.Component {
  render() {
    // Pega o estado atual da ContextStore
    let context = dispatcher.stores.ContextStore.getState();
    // Pega o parametro slug da rota
    let slug = context.getIn(['route', 'params', 'slug']);

    // Pega o estado atual da ProductStore
    let ProductStore = dispatcher.stores.ProductStore.getState();
    // Pega o produto com o slug da rota
    let product = ProductStore.get(slug);

    let productName = product ? product.name : 'carregando...';

    return (
      <div>
        <h1>Essa é a página do produto: {productName}</h1>
      </div>
    );
  }
}

export default ProductPage;

```

Veja que estamos usando a função `getIn`. Isso é um método de objetos do Immutable.

> Mas o quê?

---

## Uma rápida explicação sobre o Immutable em 30 segundos

Todas as stores fornecidas pelo SDK usam a biblioteca [Immutable](http://facebook.github.io/immutable-js/). Como o nome já dá pistas, ela permite criar objetos imutáveis. Com isso ganhamos duas vantagens:

1. Comparação de objetos de forma extremamente eficiente (em tempo O(1))
2. Segurança de que nenhuma outra parte do código vai alterar o objeto que você está usando

Imagine o seguinte objeto da ContextStore:

```js
var context = ContextStore.getState();
// {
//   "accountName": "basedevmkp",
//   "route": {
//     "params": {
//       "slug": "short-balneario"
//     }
//   }
// }
```

Para pegarmos o valor da propriedade accountName:

Em um JSON| Em um objeto Immutable
---|---
`context.accountName`|`context.get('accountName')`

Para pegarmos o valor da propriedade slug:

Em um JSON| Em um objeto Immutable
---|---
`context.route.params.slug`|`context.getIn(['route', 'params', 'slug'])`

Para este guia, essas informações são o suficiente. Porém, existem outros métodos bastante úteis: você pode ler sobre eles na [documentação do Immutable](http://facebook.github.io/immutable-js/docs/).

---

Finalmente, abra a página no browser e veja o nome na tela:

[http://basedevmkp.local.myvtex.com:3000/short-balneario/p](http://basedevmkp.local.myvtex.com:3000/short-balneario/p)

Conseguimos!

Vamos criar um link para a home para que possamos testar mais facilmente.

Copie o código:

```js
import React from 'react';
import { dispatcher } from 'sdk';
// Importa o component Link fornecido pelo React Router
import { Link } from 'react-router';

class ProductPage extends React.Component {
  render() {
    // Pega o estado atual da ContextStore
    let context = dispatcher.stores.ContextStore.getState();
    // Pega o parametro slug da rota
    let slug = context.getIn(['route', 'params', 'slug']);

    // Pega o estado atual da ProductStore
    let ProductStore = dispatcher.stores.ProductStore.getState();
    // Pega o produto com o slug da rota
    let product = ProductStore.get(slug);

    let productName = product ? product.name : 'carregando...';

    return (
      <div>
        <h1>Essa é a página do produto: {productName}</h1>
        <Link to="home">Ir para a home</Link>
      </div>
    );
  }
}

export default ProductPage;

```

O componente link gera uma tag `<a>` com o atributo `href` para a URL da rota, porém, ele intercepta o comportamento do browser e faz com que apenas mude o componente React renderizado na página. Veja funcionando no browser!

Também precisamos de um link na home para a página de produto.

Copie o código no arquivo `src/pages/HomePage.jsx`:

```js
import React from 'react';
import style from 'styles/style.less'; // eslint-disable-line
import { Link } from 'react-router';

class HomePage extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello world!</h1>
        <Link to="product" params={{slug: 'short-balneario'}}>Ver produto Short Balneário</Link>
      </div>
    );
  }
}

export default HomePage;

```

Para linkar para a página de produto, precisamos informar alguns dados para que o componente `Link` consiga montar a URL.

Legal, agora você pode ir de uma página pra outra de forma rápida.

Entretanto, temos um bug! Siga os passos para reproduzir:

- Abra a página home
- De um refresh no browser
- Navegue até a página de produto
- O página de produto mostra "carregando..." e não mostra a página de produto

> Por que isso acontece?

Quando o usuário carrega a página de produto, devido ao `resourceBinding` da rota, o servidor coloca os dados na página, o SDK pega esses dados e coloca na "ProductStore". Porém, quando o usuário carrega a página home, como ela não tem nenhum `resourceBinding`, o servidor não coloca nenhum dado na página e com isso, a "ProductStore" fica vazia.



```js
import React from 'react';
import { dispatcher } from 'sdk';
// Importa o component Link fornecido pelo React Router
import { Link } from 'react-router';

class ProductPage extends React.Component {
  // Define o state default do component
  state = {
    // Pega o estado atual da "ProductStore"
    ProductStore: dispatcher.stores.ProductStore.getState()
  }

  componentWillMount() {
    // Escuta as mudanças da "ProductStore"
    dispatcher.stores.ProductStore.listen(this.onChange);

    // Pega o contexto do site
    let context = dispatcher.stores.ContextStore.getState();
    // Pega o pathname da rota
    let pathname = context.getIn(['route', 'pathname']);

    // Caso a "ResourceStore" não tenha os resources da pagina carregado
    if (!dispatcher.stores.ResourceStore.getState().get(pathname)) {
      // Pega os parametros da rota
      let params = context.getIn(['route', 'params']).toJS(); // { slug: 'short-balneario'}
      // Pede os resources da página "product" passando os parâmetros necessários (slug)
      dispatcher.actions.ResourceActions.getRouteResources(pathname, 'product', params);
    }
  }

  componentWillUnmount() {
    // Para de escutar as mudanças, componente está saindo da tela
    dispatcher.stores.ProductStore.unlisten(this.onChange);
  }

  onChange = () => {
    // Muda o estado do componente, isso fará com que ele renderize novamente
    this.setState({
      ProductStore: dispatcher.stores.ProductStore.getState()
    });
  }

  render() {
    // Pega o estado atual da ContextStore
    let context = dispatcher.stores.ContextStore.getState();
    // Pega o parametro slug da rota
    let slug = context.getIn(['route', 'params', 'slug']);

    // Pega o produto com o slug da rota
    let product = this.state.ProductStore.get(slug);

    let productName = product ? product.name : 'carregando...';

    return (
      <div>
        <h1>Essa é a página do produto: {productName}</h1>
        <Link to="home">Ir para a home</Link>
      </div>
    );
  }
}

export default ProductPage;

```
