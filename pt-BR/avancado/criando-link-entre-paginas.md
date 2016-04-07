# Criando um link entre as páginas

Vamos criar um link para a home para que possamos testar mais facilmente.

Substitua o código do arquivo `src/components/ProductPage/ProductPage.js` por:

```js
import React from 'react';
import { stores } from 'sdk';

// Importa o component React "Link" fornecido pelo SDK
const Link = stores.ComponentStore.getState().getIn(['Link@vtex.storefront-sdk', 'constructor']);

class ProductPage extends React.Component {
  render() {
    // Pega o parametro slug da rota
    let slug = this.props.params.slug;

    // Pega o estado atual da ProductStore
    let ProductStore = stores.ProductStore.getState();
    // Pega o produto com o slug da rota
    let product = ProductStore.get(slug);

    return (
      <div>
        <h1>Essa é a página do produto: {product.name}</h1>
        <Link to="/">Ir para a home</Link>
      </div>
    );
  }
}

export default ProductPage;
```

O componente link gera uma tag `<a>` com o atributo `href` para a URL da rota, porém intercepta o comportamento do browser e faz com que apenas o componente React renderizado na página mude. Veja funcionando no browser!

Também precisamos de um link na home para a página de produto.

Copie e cole o código abaixo no arquivo `src/components/HomePage/HomePage.js`:

```js
import React from 'react';
import './HomePage.less';
import HelloWorld from 'components/HelloWorld/HelloWorld';

const Link = stores.ComponentStore.getState().getIn(['Link@vtex.storefront-sdk', 'constructor']);

class HomePage extends React.Component {
  render() {
    return (
      <div>
        <HelloWorld />
        <p className="message">Crie, construa, inove!</p>
        <Link to="/moto-x/p">Ver produto Moto X</Link>
      </div>
    );
  }
}

export default HomePage;

```

Para fazer o link para a página de produto, precisamos informar alguns dados para que o componente `Link` consiga montar a URL.

Legal, agora você pode ir de uma página pra outra de forma rápida.

---

## Recapitulando

Você completou o "Criando um link entre as páginas"! Você aprendeu a usar o componente `Link` para navegar entre páginas.

---

## Próximos passos

Agora vamos aprender a [salvar dados no servidor](/salvando-dados-no-servidor.md).
