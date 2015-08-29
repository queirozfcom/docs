# Criando um editor

Nesse guia vamos aprender a fazer um componente Banner em que o usuário pode trocar a imagem usando uma interface amigável. As interfaces de edição de componentes são chamadas de editors.

O que nos deixa animado sobre os editors é a possibilidade do desenvolvedor da loja ter autonomia para criar interfaces administrativas da maneira que achar melhor.

### Instalando o Storefront Editor

Primeiro vamos instalar o app "storefront-editor", ele é responsável por gerar toda a interface de edição. Para instalar abra a URL:

[http://basedevmkp.beta.myvtex.com/admin/gallery#/apps](http://basedevmkp.beta.myvtex.com/admin/gallery#/apps)

Abra a URL da loja:

[http://basedevmkp.local.myvtex.com:3000/](http://basedevmkp.local.myvtex.com:3000/)

É possivel visualizar a interface do Storefront Editor, os lojistas poderão editar a loja clicando no ícone de lápis no canto direito. Nesse momento, nada acontece se clicarmos nesse botão. Vamos construir o primeiro componente editável para que algo aconteça.

### Criando o componente Banner

Vamos criar um componente React para o Banner. Crie o arquivo `src/components/Banner.jsx` e copie o seguinte código:

```js
import React from 'react';

class Banner extends React.Component {
  render() {
    let imageUrl = 'http://i.imgur.com/jbBNeR3.jpg';

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

Vá para o componente `src/pages/HomePage.jsx` e copie o código:

```js
import React from 'react';
import style from 'styles/style.less'; // eslint-disable-line
import { Link } from 'react-router';
// Importa o componente Banner
import Banner from 'components/Banner';

class HomePage extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello world!</h1>

        <Banner/>

        <Link to="product" params={{slug: 'short-balneario'}}>Ver produto Short Balneário</Link>
      </div>
    );
  }
}

export default HomePage;
```

Mudamos o componente "HomePage" para que o "Banner" seja exibido na tela, confira em: [http://basedevmkp.local.myvtex.com:3000/](http://basedevmkp.local.myvtex.com:3000/)

## Transformando um componente comum em editável

Para que o Storefront Editor consiga identificar componentes editáveis na página precisamos fazer duas coisas:

- Criar a definição de componente em `storefront/components/`
- Registrar o componente para que outra parte do código consiga usar o componente
- Usar a anotação "editable" fornecida pelo SDK
- Adicionar informações ao componente React

### Criando o arquivo de definição do componente

Já aprendemos a criar um arquivo de definição de um componente com rotas em [Criando uma nova página](3-criando-uma-nova-pagina.md#criando-o-arquivo-de-definição-do-componente).

Nesse caso a definição desse componente será ainda mais simples, crie o arquivo `storefront/components/Banner.json` com:

```
{
  "assets": [
    "my-first-app.js"
  ]
}
```

### Registrando o componente

Você pode ler como registrar um componente em [Criando uma nova página](3-criando-uma-nova-pagina.md#registrando-um-componente).

### Usando "editable" e adicionando informações ao componente

Vamos agora aprender a usar a anotação "editable".

Copie o seguinte código no arquivo `src/components/Banner.jsx`:

```js
import React from 'react';
// Importa a anotação "editable" e o "dispatcher" do SDK
import { editable, dispatcher } from 'sdk';

// Anota a classe Banner com "editable" passando o "dispatcher" como parâmetro
@editable(dispatcher)
class Banner extends React.Component {
  // Definimos algumas propriedades necessárias para que o Storefront Editor consiga fazer a mágica
  static storefront = {
    // O valor da propriedade "name" deve ser o mesmo valor da propriedade name no momento do registro do componente
    name: 'Banner@vtex.my-first-app',
    // Esse é o nome que o lojista vai ver na interface para identificar o componente
    title: 'Banner'
  }

  render() {
    let imageUrl = 'http://i.imgur.com/jbBNeR3.jpg';

    return (
      <div className="banner">
        <img src={imageUrl} height={200}/>
      </div>
    );
  }
}

export default Banner;
```

Abra a URL: [http://basedevmkp.local.myvtex.com:3000/](http://basedevmkp.local.myvtex.com:3000/) e clique no botão de edição. Veja que o Storefront Editor agora consegue identificar o seu componente como editável.

## Criando o componente de edição

Vamos criar nosso primeiro componente na pasta `src/editors/`. Crie o componente chamado `BannerEditor.jsx` com o código:

```js
import React from 'react';

class BannerEditor extends React.Component {
  render() {
    // Esse é o componente que exibe os botões de "Cancelar" e "Salvar" do Storefront Editor
    // Um editor deve sempre renderizar esse componente
    let ActionBar = this.props.actionBar;

    return (
      <div>
        <img src="http://i.imgur.com/jbBNeR3.jpg" height={200}/>

        <form>
          <label htmlFor="url">URL da imagem</label>
          <input id="url" className="form-control" type="url" placeholder="URL"/>
        </form>

        <ActionBar/>
      </div>
    );
  }
}

export default BannerEditor;
```

É definido por convenção que todos os componentes editors tenham o nome com o sufixo "Editor", ex: "BannerEditor".

Vamos registrar o componente de edição no arquivo `src/my-first-app-editor.jsx` para que o Storefront Editor consiga acessá-lo. Copie o código:

```js
import BannerEditor from 'editors/BannerEditor';
import { dispatcher } from 'sdk';

let components = [
  {
    name: 'BannerEditor@vtex.my-first-app',
    constructor: BannerEditor
  }
];

dispatcher.actions.ComponentActions.register(components);
```

Abra a URL: [http://basedevmkp.local.myvtex.com:3000/](http://basedevmkp.local.myvtex.com:3000/) e clique no botão de edição. O componente de edição será aberto na tela.

### Salvando configurações

Como está agora, o editor não edita nada no site. Precisamos salvar o formulário do editor em algum lugar. A Gallery é justamente um repositório de configurações, ela é perfeita para isso! Vamos incrementar os componentes para salvar as configurações do Banner lá.

Para isso, o Banner deve ter um identificador único na Gallery para que ninguém sobrescreva essas configurações.

#### Atribuindo um identificador ao componente Banner

Altere o método `render` da "HomePage":

```js
render() {
  return (
    <div>
      <h1>Hello world!</h1>

      <Banner id="banner-1" route="home"/>

      <Link to="product" params={{slug: 'short-balneario'}}>Ver produto Short Balneário</Link>
    </div>
  );
}
```

Observe que atribuímos o id "banner-1" e passamos o nome da rota da página. Esses dois parâmetros (`id` e `route`) formam a identificação única do componente no Storefront.

#### Ajustando o componente editor

Vamos alterar o componente "BannerEditor" para que ele salve as configurações na Gallery.

```js
import React from 'react';
import { dispatcher } from 'sdk';

class BannerEditor extends React.Component {
  constructor(props) {
    super(props);

    // O componente editor recebe as configurações do componente que está editando como props
    let settings = this.props.settings;
    this.state = {
      imageUrl: settings ? settings.get('imageUrl') : 'http://i.imgur.com/jbBNeR3.jpg'
    };
  }

  handleSave = () => {
    // O componente editor recebe uma função que salva as configurações do componente na Gallery como props
    this.props.saveSettings(this.state);
  }

  changeImageUrl = (e) => {
    let value = e.target.value;
    this.setState({ imageUrl: value });
  }

  render() {
    // O componente "ActionBar" tem a prop "onSave" que chama a função passada como parâmetro
    // quando o usuário clica em "Salvar"
    let ActionBar = this.props.actionBar;

    return (
      <div>
        <img src={this.state.imageUrl} height={200}/>

        <form>
          <label htmlFor="url">URL da imagem</label>
          <input id="url" className="form-control" type="url"
                 value={this.state.imageUrl} onChange={this.changeImageUrl} placeholder="URL"/>
        </form>

        <ActionBar onSave={this.handleSave.bind(this)}/>
      </div>
    );
  }
}

export default BannerEditor;
```

Note que fizemos três coisas:
- Usamos a prop "settings" para exibir as configurações atuais do Banner
- Criamos uma função (`this.handleSave`) que será chamada ao clicar no botão "Salvar"
- Usamos a prop "saveSettings" para salvar as configurações do componente na Gallery

#### Exibindo as configurações do Banner

Por fim, vamos pegar as configurações salvas na Gallery e usá-las no componente.

```js
import React from 'react';
import { editable, dispatcher } from 'sdk';

@editable(dispatcher)
class Banner extends React.Component {  
  static storefront = {
    name: 'Banner@vtex.my-first-app',
    title: 'Banner'
  }

  render() {
    let settings = this.props.settings;
    let imageUrl = settings ? settings.get('imageUrl') : 'http://i.imgur.com/jbBNeR3.jpg';

    return (
      <div className="banner">
        <img src={imageUrl} height={200}/>
      </div>
    );
  }
}

export default Banner;
```

O componente com a anotação "editable" recebe suas configurações automaticamente pela prop "settings".

---

Você completou o "Criando um editor"!
