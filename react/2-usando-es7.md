# Usando ES7

## Alterando algumas configurações

Vamos alterar algumas coisas para que possamos usar o ES7.

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

## Entendendo ES7

Veja que estamos usando `class`, `import`, `export` e outras coisas muito legais do ES7, versão do Javascript que será lançada em 2016.

### import

```js
import React from 'react/addons';
import 'normalize.css';
import '../styles/main.css';
import imageURL from '../images/yeoman.png';
```

Para importar módulos use a sintaxe `import`. Leia mais sobre ela na documentação da Mozilla:

[Artigo sobre import no MDN](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Statements/import)

### export

```js
export default TesteApp;
```

Junto com o `import`, devemos usar o `export`. Leia mais sobre ela na documentação da Mozilla:

[Artigo sobre export no MDN](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Statements/export)


### class

```js
class TesteApp extends React.Component {
```

Javascript agora provê classes de forma nativa. Leia mais sobre ela na documentação da Mozilla:

[Artigo sobre class no MDN](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Statements/class)

---

Você completou o "Usando ES7"! Agora vamos introduzir alguns conceitos do React.

Próximo passo: [Conceitos do React](3-conceitos-do-react.md)
