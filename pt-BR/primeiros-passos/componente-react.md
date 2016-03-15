# Componente React

Vamos criar nosso primeiro componente React no Storefront. Esse componente será responsável pela renderização da home.

Crie a pasta `storefront`. Tudo que estiver dentro dessa pasta será interpretado pelo Storefront (app "vtex.storefront"). Iremos pouco a pouco apresentando o que o Storefront oferece e quais pastas e arquivos devem ser criados.

Crie a pasta `assets` dentro da pasta `storefront`.

Você deve ter algo assim:

```sh
.
├── meta.json
└── storefront/
    └── assets/
```

Em `assets` devem ficar todos os arquivos Javascript, CSS, imagens e fontes. Crie o arquivo `HomePage.jsx` dentro dela com um componente React simples:

### `HomePage.jsx`

```js
class HomePage extends React.Component {
  render() {
    return (
      <div><h1>Hello world!</h1></div>
    );
  }
}
```

Como ele é um arquivo que contém código JSX, devemos compila-lo.

Instale o babel com: `npm install babel-cli`. É necessário também instalar um pacote extra para habilitar a integração com o React: `npm install babel-preset-react`.

Para compilar o arquivo digite:

```sh
babel ./storefront/assets/**.jsx --out-dir .
```

O Babel gera o arquivo `HomePage.js` com o código compilado.

## Recapitulando

Na plataforma VTEX existem apps de serviço, o Storefront é um deles. Um app de serviço exerce suas funções apenas nos arquivos que estão dentro de sua pasta. A pasta `storefront` possui sua estrutura própria.

Na pasta `storefront/assets/` ficam todos os arquivos estáticos de seu app que serão consumidos pelo Storefront.

Criamos um arquivo Javascript que usa novos recursos da linguagem Javascript (ES6) e JSX. Compilamos usando o Babel para Javascript atual (ES5).

---

### Próximos Passos

Criamos nosso primeiro asset, um componente React. Vamos agora criar o [descritor do componente](descritor-de-componente.html).
