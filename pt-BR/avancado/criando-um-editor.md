# Criando um editor

---
### Atenção

Esta documentação foi feita baseada na versão _beta_ (**não finalizada**) do [Editor](https://github.com/vtex-apps/editor), esta versão está em fase de testes, pode apresentar inconsistências e ser modificada sem aviso prévio.

---

Nesse guia vamos aprender a fazer um componente Banner em que o usuário pode trocar a imagem usando uma interface amigável. As interfaces de edição de componentes são chamadas de editors.

O que nos deixa animados sobre os editors é a possibilidade do desenvolvedor da loja ter autonomia para criar interfaces administrativas da maneira que achar melhor.

### Instalando o Editor

Primeiro vamos instalar o app "editor", ele é responsável por gerar toda a interface de edição. Para instalar abra a URL:

[http://sualoja.beta.myvtex.com/admin/app-store](http://sualoja.beta.myvtex.com/admin/app-store)

Abra a URL da loja:

[http://sualoja.local.myvtex.com:3000/admin/storefront](http://sualoja.local.myvtex.com:3000/admin/storefront)

É possível visualizar a interface de customização da loja, os lojistas poderão editar a loja clicando nos _placeholders_ destacados com cor azul. O botão de lápis no canto direito muda o estado de visualização.

Nos passos seguintes vamos construir um componente editável da página.

### Criando o componente Banner

Vamos criar um componente React para o Banner. Crie o arquivo `src/components/Banner/Banner.js` e copie o seguinte código:

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

Vá para o componente `src/components/HomePage/HomePage.js` e copie o código:

```js
import React from 'react';
import { stores } from 'sdk';
import './HomePage.less';
import HelloWorld from 'components/HelloWorld/HelloWorld';

const Link = stores.ComponentStore.getState().getIn(['Link@vtex.storefront-sdk', 'constructor']);

class HomePage extends React.Component {
  render() {
    return (
      <div>
        <Placeholder id="banner"/>
        <HelloWorld />
        <p className="message">Crie, construa, inove!</p>
        <Link to="/short-balneario/p">Ver produto Short Balneário</Link>
      </div>
    );
  }
}

export default HomePage;
```

### Configurando um ponto de extensão

Conforme aprendemos na configuração de um [placeholder](/avancado/placeholders.md) vamos adicionar um componente para ocupar a sua área.

Crie o arquivo `storefront/settings/routes/home/HomePage@mycompany.my-first-app/banner.json`

```json
{
  "component": "Banner@mycompany.my-first-app",
}
```

## Transformando um componente comum em editável

Para que o Editor consiga identificar componentes editáveis na página precisamos fazer duas coisas:

- Criar a definição de componente em `storefront/components/`
- Registrar o componente com `ComponentActions.register` para que outra parte do código consiga usar o componente
- Usar o decorador `@editable` fornecido pelo Editor

### Criando o arquivo de definição do componente

Já aprendemos a criar um arquivo de definição de um componente com rotas em [Criando uma nova página](/criando-uma-nova-pagina.md#criando-o-arquivo-de-definição-do-componente).

Nesse caso a definição desse componente será ainda mais simples, crie o arquivo `storefront/components/Banner.json` com:

```
{
  "assets": [
    "common.js",
    "Banner.js",
    "editors/index.js"
  ]
}
```

### Registrando o componente

Precisamos [registrar](/criando-uma-nova-pagina.md#registrando-um-componente) o componente "Banner" no arquivo `src/components/Banner/index.js`.
Lembrando que o mesmo deve ser feito com o componente `HomePage`.

```js
import { actions } from 'sdk';
import Banner from 'components/Banner/Banner';

let component = [
  {
    name: 'Banner@mycompany.my-first-app',
    constructor: Banner
  }
];

actions.ComponentActions.register(component);
```

### Adicione ao `webpack.config.js`

```js
{...}

var config = {
  entry: {
    'HomePage': ['./src/components/HomePage/index.js'],
    'Banner': ['./src/components/Banner/index.js'],
    'editors/index': ['./src/editors/index.js']
  }
}

{...}
```

### Usando `@editable` e adicionando informações ao componente

Vamos agora aprender a usar o decorador `@editable`.

Copie o seguinte código no arquivo `src/components/Banner/Banner.js`:

```js
import React from 'react';
// Importa o decorador "editable" do SDK
import { editable } from 'vtex-editor';

// Decora a classe "Banner" com "editable"
@editable ({
  name: 'Banner@mycompany.my-first-app', // Deve ser o mesmo valor da propriedade "name" no momento do registro do componente
  title: 'Banner', // Nome do componente que será apresentado para o usuário (lojista)
  editable: true // indica que o componente é editável
})
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

Abra a URL: [http://sualoja.local.myvtex.com:3000/admin/storefront](http://sualoja.local.myvtex.com:3000/admin/storefront) e clique em cima do componente. Veja que o Editor agora consegue identificar o seu componente como editável.

## Criando o componente de edição

Vamos criar nosso primeiro componente na pasta `src/editors/BannerEditor/`. Crie o componente chamado `BannerEditor.js` com o código:

```js
import React from 'react';

class BannerEditor extends React.Component {
  render() {
    // Esse é o componente que exibe os botões de "Cancelar" e "Salvar" do Editor
    // Um editor deve sempre renderizar esse componente
    let ActionBar = this.props.actionBar;

    return (
      <div>
        <img src="http://i.imgur.com/jbBNeR3.jpg" height={200}/>

        <form>
          <label htmlFor="url">URL da imagem</label>
          <input id="url" className="form-control" type="url" placeholder="URL"/>
        </form>

        <ActionBar id={this.props.componentProps.id} title={this.props.title}/>
      </div>
    );
  }
}

export default BannerEditor;
```

É definido por convenção que todos os componentes editors tenham o nome com o sufixo "Editor", ex: "BannerEditor".

Vamos registrar o componente de edição no arquivo `src/editors/index.js` para que o Editor consiga acessá-lo. Copie o código:

```js
import { actions } from 'sdk';
import BannerEditor from './BannerEditor/BannerEditor';

let components = [
  {
    name: 'BannerEditor@mycompany.my-first-app',
    constructor: BannerEditor
  }
];

actions.ComponentActions.register(components);
```

Abra a URL: [http://sualoja.local.myvtex.com:3000/admin/storefront](http://sualoja.local.myvtex.com:3000/admin/storefront) e clique sobre o componente na página. O componente de edição será aberto na tela lateral esquerda.

### Salvando configurações

Como está agora, o editor não edita nada no site. Precisamos salvar o formulário do editor em algum lugar. A Gallery é justamente um repositório de configurações, ela é perfeita para isso! Vamos incrementar os componentes para salvar as configurações do Banner lá.

#### Ajustando o componente editor

Vamos alterar o componente "BannerEditor" para que ele salve as configurações na Gallery.

```js
import React from 'react';

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
          <input
            id="url"
            className="form-control"
            type="url"
            value={this.state.imageUrl}
            onChange={this.changeImageUrl}
            placeholder="URL"
          />
        </form>

        <ActionBar id={this.props.componentProps.id} onSave={this.handleSave.bind(this)}/>
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
import { editable } from 'editor';

@editable({
  name: 'Banner@mycompany.my-first-app',
  title: 'Banner',
  editable: true
})
class Banner extends React.Component {
  render() {
    let imageUrl = 'http://i.imgur.com/jbBNeR3.jpg';

    // Pega as configurações do componente
    if (this.props.settings) {
      imageUrl = this.props.settings.get('imageUrl');
    }

    return (
      <div className="banner">
        <img src={imageUrl} height={200}/>
      </div>
    );
  }
}

export default Banner;
```

O componente com a decorador `@editable` recebe suas configurações automaticamente pela prop `settings`.

---

## Recaptulando

Aprendemos como criar um componente editável e carregá-lo na interface para o usuário, também descobrimos como atualizar o conteúdo dos nossos componentes após a atualização das suas configurações.