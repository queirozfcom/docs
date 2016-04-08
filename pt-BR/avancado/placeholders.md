# Placeholders

Um **placeholder** é um _ponto de extensão_ entre apps. Basicamente ele determina um lugar na página onde componentes poderão entrar.

Os placeholders permitem que desenvolvedores componham suas apps com apps de terceiros ao mesmo tempo que dá liberdade para o usuário substituí-las.

### Criando um placeholder para o Banner

Vamos criar um componente React para o Banner. Crie o arquivo `src/components/Banner/Banner.js` e copie o seguinte código:

```js
import React from 'react';

class Banner extends React.Component {

  constructor(props) {
    super(props);
    this.state = this.props.settings ? this.props.settings.toJS() : {};
  }

  render() {
    let imageUrl = this.state.imageUrl;

    return (
      <div className="banner">
        <img src={imageUrl} height={200}/>
      </div>
    );
  }
}

export default Banner;
```

É um componente simples que exibe uma imagem.

Vá para o componente `src/components/HomePage/HomePage.js` e copie o código:

```js
import React from 'react';
import { stores } from 'sdk';

const Placeholder = stores.ComponentStore.state.getIn(['Placeholder@vtex.storefront-sdk', 'constructor']);

class HomePage extends React.Component {

  render() {
    return (
      <div className="theme">
        <Placeholder id="banner"/>
      </div>
    );
  }
}

export default HomePage;
```

Você está criando um espaço (`placeholder`) no componente HomePage que pode ser preenchido por um componente com `id` "banner".

### Descrevendo o componente
É preciso [descrever](primeiros-passos/descritor-de-componente) os componentes "HomePage"
e "Banner".

`storefront/componentes/HomePage.json`
```json
{ 
  "assets": [
    "common.js",
    "HomePage.js"
  ]
}
```

`storefront/componentes/Banner.json`
```json
{
  "assets": [
    "common.js",
    "Banner.js"
  ]
}
```

### Registrando o componente

Precisamos [registrar](3-criando-uma-nova-pagina.md#registrando-um-componente) os componentes "HomePage" e Banner".


`src/components/HomePage/index.js`
```js
import { actions } from 'sdk';
import HomePage from './HomePage';

let component = [
  {
    name: 'HomePage@mycompany.my-first-app',
    constructor: HomePage
  }
];

actions.ComponentActions.register(component);
```

`src/components/Banner/index.js`
```js
import { actions } from 'sdk';
import Banner from './Banner';

let component = [
  {
    name: 'Banner@mycompany.my-first-app',
    constructor: Banner
  }
];

actions.ComponentActions.register(component);
```

### Registrando o componente Root

Precisamos [registrar o componente Root](primeiros-passos/root.md) e [configurar o componente HomePage](3-criando-uma-nova-pagina.md) para rota "home".

### Configurando um ponto de extensão

Todo placeholder deve obrigatoriamente ter um **id** único. O identificador possibilita
que um ponto específico na página seja reconhecido e configurado por qualquer app. Neste caso o valor do id é "banner".

Crie o arquivo `storefront/settings/routes/home/HomePage@mycompany.my-first-app/banner.json`

```json
{
  "component": "Banner@mycompany.my-first-app",
  "settings": {
      "imageUrl": "http://i.imgur.com/jbBNeR3.jpg"
  }
}
```

Você está criando uma **configuração padrão** para um placeholder da sua app.

O trecho acima significa que na rota _"home"_ no componente _"HomePage@mycompany.my-first-app"_ o placeholder de id _"banner"_ é ocupado pelo componente _"Banner@mycompany.my-app"_.

É importante dizer que estas configurações podem ser sobrescritas pelo usuário, desde que tenha um editor que permita fazer isso. 

### Visualizando alterações

Digite no terminal o comando `vtex watch -s` e abra a URL [http://sualoja.local.myvtex.com:3000/](http://sualoja.local.myvtex.com:3000/). Você deve visualizar a imagem da configuração do banner renderizada.

---

## Recapitulando

O _placeholder_ é um recurso fundamental para a extensibilidade do Storefront, sua função é marcar um lugar na página onde componentes poderão entrar.

Esta flexibilidade permite a troca rápida de componentes entre diferentes apps em uma página. Para isso, basta alterar a configuração do placeholder que é vinculalda a um `id` único por página.

Toda app pode ter **configurações padrão** para os seus componentes, portanto, qualquer placeholder recebe uma configuração padrão que poderá ser alterada pelo usuário através de um editor.