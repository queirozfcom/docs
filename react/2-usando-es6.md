# Usando ES6

## Alterando algumas configurações

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

## Entendendo ES6

Veja que estamos usando `class`, `import`, `export` e outras coisas muito legais do ES6, versão do Javascript que foi lançada em 2015.

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

Você completou o "Usando ES6"! Agora vamos introduzir alguns conceitos do React.

Próximo passo: [Conceitos do React](3-conceitos-do-react.md)
