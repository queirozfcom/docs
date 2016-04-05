# Pegando dados do servidor

Temos duas páginas: a home e a página de produto.

> Mas o que é uma pagina de produto sem produtos?

Vamos aprender a pegar dados da API pra preencher essa página.

### Criando o arquivo de definição do componente

Copie o JSON e coloque no arquivo `storefront/components/ProductPage.json`:

```json
{
  "resourceBindings": [
    {
      "locator": "search@vtex.storefront-sdk",
      "relativePath": "/{{ account }}/products/{{ route.slug }}",
      "bindTo": "product@vtex"
    }
  ],
  "assets": [
    "common.js",
    "ProductPage.js"
  ]
}
```

Veja que inserimos uma nova propriedade chamada `resourceBindings`. Os parâmetros que ela recebe são:

- **locator**: identificador do resource que será usado. Neste caso estamos usando um resource do SDK chamado ["search"](https://github.com/vtex-apps/storefront-sdk/blob/master/storefront/resources/search.json), responsável por prover o base-endpoint da chamada.

- **relativePath**: é o complemento necessário para a URL de locator definida. 
  * Os paths também podem conter **variáveis**:  _"/\{\{ account }}/products/\{\{ route.slug }}/"_

Imagine que você tem uma API com a URL `http://minhapi.com.br`, o `relativePath` complementa essa URL tendo como resultado `http://minhaapi.com.br/acount-name-da-loja/nome-do-produto`.

- **bindTo**: É o nome da chave que o resource irá receber na store do Storefront SDK.

- **queryParams**: São os parametros que serão repassados na query string durante a chamada.
  * Aqui também é possível o uso de **variáveis**:

```json
"queryParams": {
  "category": "{{ route.splat }}",
  "brands": "{{ query.brands }}"
}
```

> O **locator** e o **relativePath** deste exemplo são baseados na [Search API](http://api.vtex.com/doc/search-api/).

> A **Search API** possui endpoints para obtenção de dados do catálogo da VTEX.

O `resourceBindings` liga uma rota a uma chamada a API. Voce pode declarar quantos `bindings` quiser, portanto, diferentes dados podem ser pré-carregados para uma mesma página.

### Sobre variáveis

Falamos sobre **variáveis** anteriormente quando mencionamos o **relativePath** e o **queryParams**, mas o que exatamente são essas variáveis e de onde elas vêm?

Abaixo temos uma tabela com uma descrição breve de cada variável disponível:

Variável|Descrição
---|---
account|Essa variável possui o valor de qual o `accountName` da loja atual.
route|Essa variável expõe valores que definidos nas rotas.
query|Essa variável expõe valores de query string das rotas.

#### Mas o que isso quer dizer?

Vamos destrinchar o `resourceBindings` que acabamos de ver:

```json
{
  "resourceBindings": [
    {
      "locator": "search@vtex.storefront-sdk",
      "relativePath": "/{{ account }}/products/{{ route.slug }}",
      "bindTo": "product@vtex"
    }
  ],
  "assets": [
    "common.js",
    "ProductPage.js"
  ]
}
```

Estamos usando as variáveis `account` e `route.slug` para compor o **relativePath**.

`account` nós já sabemos que se refere ao `accountName` atual, mas o que é esse `slug` dentro de `route`?

Você se lembra que a descrição dizia que o route expõe valores definidos nas rotas? Então, o slug é um desses valores.

O arquivo de rota atual deve ter o seguinte conteúdo:
```json
{
  "path": "/:slug/p"
}
```

Se o valor se chamasse `:product`, usariámos `route.product` para acessar esse valor em nosso `resourceBindings`.

Já o **queryParams** serve para as query strings da rota! Se estamos na nossa rota de produto atual e ela possui uma ou mais query strings, podemos acessar esse valores usando a variável **query**.

**Exemplo**:

Vamos supor que nossa página de produto tem uma cor diferente se alguém altera o valor da query string **color**. Teríamos uma URL mais ou menos assim para acessar a página na cor vermelha: `/moto-x/p?color=red`.

Para acessarmos esse valor digitamos `query.color`.

E para finalizar, esses valores também ficam disponíveis na página através da prop **params** (`props.params`).

---

Carregue a página de produto no browser ([http://sualoja.local.myvtex.com:3000/moto-x/p](http://sualoja.local.myvtex.com:3000/moto-x/p)), clique com o botão direito do mouse e veja o código fonte. Você pode ver que os dados do produto estão impressos na página. O SDK pega esses dados automaticamente e os insere dentro da store "ProductStore".

### Criando o componente React da página

Vamos fazer com que o nosso código React acesse essa store e imprima o nome do produto na página.

Copie o seguinte código e coloque no arquivo `src/pages/ProductPage/ProductPage.js`:
```js
import React from 'react';
import { stores } from 'sdk';

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
      </div>
    );
  }
}

export default ProductPage;

```

Veja que estamos usando a função `get`. Isso é um método de objetos do Immutable.

> Mas o quê?

---

## Uma rápida explicação sobre o Immutable em 30 segundos

Todas as stores fornecidas pelo SDK usam a biblioteca [Immutable](http://facebook.github.io/immutable-js/). Como o nome já indica, ela permite criar objetos imutáveis. Com isso ganhamos duas vantagens:

1. Comparação de objetos de forma extremamente eficiente (em tempo [O(1)](https://en.wikipedia.org/wiki/Analysis_of_algorithms#Orders_of_growth))
2. Segurança de que nenhuma outra parte do código vai alterar o objeto que você está usando

Imagine o seguinte objeto da ProdutStore:

```js
var products = ProductStore.getState();
// {
//   "camisa-polo": {
//     "name": "Camisa Polo",
//     "slug": "camisa-polo",
//     "brand": {
//       "name": "Lacoste",
//       "slug": "lacoste"
//     }
//     ...
//   },
//   "meia-branca": {
//     "name": "Meia branca",
//     "slug": "meia-branca",
//     ...
//   }
// }
```

Para pegarmos os dados do produto "camisa-polo":

Em um JSON| Em um objeto Immutable
---|---
`products["camisa-polo"]`|`products.get('camisa-polo')`

Para pegarmos o nome da marca da "camisa-polo":

Em um JSON| Em um objeto Immutable
---|---
`products["camisa-polo"].brand.name`|`products.getIn(['camisa-polo', 'brand', 'name'])`

Para este guia, essas informações são o suficiente. Porém, existem outros métodos bastante úteis: você pode ler sobre eles na [documentação do Immutable](http://facebook.github.io/immutable-js/docs/).

---

Finalmente, abra a página no browser e veja o nome na tela:

[http://sualoja.local.myvtex.com:3000/moto-x/p](http://sualoja.local.myvtex.com:3000/moto-x/p)

Conseguimos!

### Criando um link entre as páginas

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

Você completou o "Pegando dados do servidor"! Você aprendeu a usar `resourceBindings` para obter dados de uma página.

---

## Próximos passos

Agora vamos aprender a [salvar dados no servidor](/salvando-dados-no-servidor.md).
