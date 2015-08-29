# Começando com react

Instale o pacote node `generator-react-webpack`:

```
npm install -g yo generator-react-webpack grunt-cli
```

Crie uma pasta para começar o projeto. Navegue até ela e rode o comando:

```
yo react-webpack
```

Responda as perguntas do generator:

- Não inclua o "react-router"
- Não use nenhuma arquitetura
- Use LESS
- Use a extensão ".jsx (deprecated)"

Ele irá instalar as dependências, isso pode levar alguns minutos.

Abra a pasta no seu editor de texto ou IDE.

## Rodando a aplicação

Para rodar a aplicação digite:

```
grunt serve
```

Ele irá buildar o projeto e abrir uma aba do seu navegador.

## Alterando algumas configurações

Abra o arquivo `webpack.config.js` e altere a linha 47 para:

```
loader: 'react-hot!babel-loader?stage=0'
```

Com isso, poderemos usar os recursos novos da linguagem Javascript.

Altere o código de `src/components/TesteApp.js` para:

```js
import React from 'react/addons';
import 'normalize.css';
import '../styles/main.css';
import imageURL from '../images/yeoman.png';

class TesteApp extends React.Component {
  render() {
    return (
      <div className="main">
        <img src={imageURL} />
      </div>
    );
  }
}

export default TesteApp;

React.render(<TesteApp />, document.getElementById('content')); // jshint ignore:line
```

Veja que estamos usando `class`, `import`, `export` e outras coisas muito legais do ES7, versão do Javascript que será lançada em 2016.

---

Você completou o "Primeiros Passos"! No próximo passo vamos entender o código.

Próximo passo: [Entendendo o código](2-entendendo-o-codigo.md)
