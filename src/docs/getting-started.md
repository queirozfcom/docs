# Getting Started

## Setup

Para começar, instale o [node](https://gist.github.com/brenoc/534729c806dc0d4ca917) em sua máquina.

Abra o terminal e instale alguns pacotes que serão úteis nesse guia:

```sh
npm install -g yo generator-vtex
npm install -g vtex
```

No caso de erro na instalação, use `sudo`.

Os pacotes yo ([Yeoman](http://yeoman.io/)) e [generator-vtex](https://github.com/vtex/generator-vtex/) são pacotes que geram a estrutura de pastas de apps automaticamente.

O pacote `vtex` é uma ferramenta que chamamos de [Toolbelt](https://github.com/vtex/toolbelt). O Toolbelt é essencial para o desenvolvimento de apps, pois permite que você publique apps na Gallery e desenvolva localmente.

Para isso e para ver suas alterações, é necessário instalar um cookie específico em seu browser. Para facilitar este processo, instale alguma extensão de edição de cookies no browser.

Caso esteja usando o Google Chrome, recomendamos a [Cookie Inspector](https://chrome.google.com/webstore/detail/cookie-inspector/jgbbilmfbammlbbhmmgaagdkbkepnijn?utm_source=chrome-app-launcher-info-dialog).

## Criando a primeira app

Vamos criar nossa primeira app no Storefront. Crie uma pasta com o nome "my-first-app" e abra o terminal nela.

Rode o seguinte comando para iniciar o `generator-vtex`:
```sh
yo vtex:storefront --simple
```

Dê o nome de sua primeira app como `my-first-app` e use `alphateam` como vendor. Este processo irá criar a estrutura de pastas e arquivos iniciais de sua App.

## Estrutura de pastas

Uma app no Storefront tem as seguintes pastas e arquivos:

```
.
├── storefront/
│   ├── assets/
│   ├── components/
│   └── resources/
├── .vtexignore
└── meta.json
```

### assets/

Aqui ficam todos os arquivos que podem ser acessados publicamente, como arquivos Javascript, CSS, imagens, SVG, fontes, etc.

### components/

Nessa pasta moram as definições de componentes usadas pelo servidor do Storefront. Veja mais na seção [blablabla](#).

### resources/

Esses arquivos definem chamadas a APIs, usaremos os recursos em arquivos de componentes e no código Javascript. Veja mais em [blablabla](#).

### meta.json

Todas as apps na Gallery precisam do arquivo `meta.json`. Nele ficam registradas diversas informações sobre sua app como o nome (`name`), nome amigável (`title`), descrição (`description`), depedências de outras apps (`dependencies`) e quais serviços são usados (`schemas`).

### .vtexignore

Esse arquivo é usado pelo Toolbelt. Aqui estão listados quais arquivos e pastas não devem ser enviados para a Gallery.

## Workspaces e Sandbox

Precisamos de duas coisas para criar um ambiente de desenvolvimento: um workspace próprio e uma sandbox.

### Workspace

Uma loja guarda diversas configurações: quais apps estão instaladas e qual imagem deve aparecer no banner da home, por exemplo. Este conjunto de configurações fica em um workspace. O workspace de produção chama-se `master`. Para fazer uma alteração no workspace de produção, é preciso fazer as alterações em um novo workspace e, em seguida, promover esse workspace para `master`.

Para desenvolvermos nossa primeira app, precisaremos criar um novo workspace.

Vá até [o admin de workspaces](http://basedevmkp.vtexcommercebeta.com.br/admin/gallery#/workspaces), clique em "Novo workspace" e crie um workspace com o seu nome.xw

### Sandbox

É um ambiente de desenvolvimento de apps. Para entender como uma sandbox funciona, devemos entender primeiro como a Gallery funciona.

Este é o fluxo de dados de uma loja no StoreFront:

1. Usuário abre uma página da loja
2. Servidor verifica quais apps estão instaladas
3. Servidor processa os arquivos das apps que estão armazenadas na Gallery
4. Servidor responde a página para o usuário

A sandbox cria uma espécie de Gallery temporária e privada para facilitar o desenvolvimento de apps. Sem ela, um desenvolvedor teria que lançar uma versão nova de sua app na Gallery e instalar a app para ver as mudanças.

Quando o desenvolvedor usa uma sandbox, o fluxo é o seguinte:

1. Usuário abre uma página da loja  
1.1 **Servidor verifica quais apps estão na sandbox**  
1.2 **Servidor processsa os arquivos das apps que estão armazenadas na Sandbox**  
2. Servidor verifica quais apps estão instaladas
3. Servidor processa os arquivos das apps que estão armazenadas na Gallery
4. Servidor responde a página para o usuário

A sandbox é ótima e ela será sua nova amiga!

### Ativando o workspace e a sandbox

Para ativar o workspace e sua sandbox você deve adicionar dois cookies em seu browser. Isso é necessário para que o servidor verifique qual é a sua sandbox e quais apps estão sendo desenvolvidos nela.

Primeiro, entre na URL da loja no ambiente de desenvolvimento:

[http://basedevmkp.beta.myvtex.com/](http://basedevmkp.beta.myvtex.com/)

Caso você tenha instalado a extensão [Cookie Inspector](https://chrome.google.com/webstore/detail/cookie-inspector/jgbbilmfbammlbbhmmgaagdkbkepnijn?utm_source=chrome-app-launcher-info-dialog), abra o Developer Tools do Chrome ("F12" ou "command+option+i") e clique na aba "Cookies", clique com o botão direito do mouse e, em seguida, em "Add new cookie".

Crie o cookie do workspace:

Nome|Valor
---|---
vtex_workspace|nomedomeuworkspace

Para criar o cookie da sandbox, vamos precisar de:

- Nome do `vendor` da app. Neste caso usaremos "alphateam"
- Nome da sua sandbox. Fique à vontade pra escolher (ele deve ser único!)
- Nome da sua app. Usaremos "my-first-app"

O formato do cookie:

Nome|Valor
---|---
vtex_sandbox|`nome-do-vendor/nome-da-sandbox=nome-da-app`

Logo, deve ficar algo assim (certifique-se de colocar o nome da sua sandbox):

Nome|Valor
---|---
vtex_sandbox|alphateam/nome-da-sandbox=my-first-app

## Hello World!

Agora que temos tudo pronto para pôr a mão na massa, vamos ver o tão esperado "Hello World!".

Abra o terminal na pasta da app e digite:

```sh
vtex watch nomedasandbox
```

Após fazer o login, verá que o Toolbelt mostrará uma linda mensagem e algo assim:

```
Watching nomedasandbox

U meta.json
U storefront/assets/index.js
U storefront/components/HomePage.json

... files uploaded
```

O que o Toobelt acabou de fazer foi:

- Ler o arquivo `meta.json` e o vendor e o nome da sua app
- Ler o arquivo `.vtexignore` e guardar quais arquivos ela não deve fazer upload
- Upload de todos os arquivos que não estão na lista de arquivos do `.vtexignore`

Estes arquivos vão parar dentro da pasta "alphateam.my-first-app", que é o identificador único de uma app dentro da sua sandbox.

Abra a URL da loja em desenvolvimento:

[http://basedevmkp.beta.myvtex.com/](http://basedevmkp.beta.myvtex.com/)

Você deve estar vendo "Hello World!" escrito na tela.

O Toolbelt está escutando qualquer modificação feita nos arquivos de sua app. Podemos testar isso abrindo o arquivo `assets/index.js` e alterando o texto "Hello World!". Salve o arquivo. Verá que o Toolbelt fez o upload para a sandbox. Note também que a página deu refresh, isso acontece automaticamente por conta do sistema de livereload.

## Melhorando o processo de desenvolvimento

Apesar de funcionar bem, essa forma de desenvolvimento pode se tornar tediosa à medida que sua app começa a crescer. Arquivos Javascript e CSS começam a se proliferar e escrever React sem JSX é bem estranho. Além disso, nosso código não está minificado e não estamos usando nenhum pré-processador de CSS, como LESS ou SASS.

Para resolver tudo isso, usamos a ferramenta de build Webpack e uma estrutura de desenvolvimento opinionada que usa ES7, eslint, LESS, react-hot-loader e Webpack:

 - ES7 é a mais recente versão do Javascript que será lançada em 2016, então já estamos escrevendo mirando para o futuro. Mas não esquecemos do IE8! Usamos o Babel, uma ferramenta que transforma o código ES7 para a versão atual do Javascript.

 - eslint é uma ferramenta que padroniza como o código deve ser escrito.

 - LESS é o pré-processador CSS escolhido pelo VTEX Lab, também um dos mais usados pela comunidade front-end.

 - O `react-hot-loader` é uma espécie de livereload 2.0 que, ao invés de recarregar toda a página, atualiza apenas o componente React que foi modificado. Isso faz com que o ciclo de desenvolvimento seja *muito* mais rápido.

 - Por fim, o Webpack agrega todas essas ferramentas e faz todas funcionarem como mágica, além de minificar imagens, SVGs, Javascript e CSS.

### Nova estrutura de pastas

Não se apague ao seu app agora, vamos apagar toda essa estrutura e começá-lo do zero com essa nova estrutura de desenvolvimento.

Apague todos os arquivos da pasta de sua app. Abra o terminal na mesma pasta e digite:

```sh
yo vtex:storefront
```

Crie a app com o nome "my-first-app", e "alphateam" como vendor.

Você verá que algumas pastas e arquivos foram criados e as dependências do node foram instaladas. Sua app agora deve parecer com isso:

```
.
├── src/
│   ├── assets/
│   ├── components/
│   ├── editors/
│   ├── pages/
│   ├── styles/
│   ├── utils/
│   ├── my-first-app-editor.jsx
│   └── my-first-app.jsx
├── storefront/
│   ├── assets/
│   ├── components/
│   └── resources/
├── .eslintrc
├── .gitignore
├── .vtexignore
├── meta.json
├── package.json
└── webpack.config.js
```

Nessa nova estrutura, escreveremos a maior parte do nosso código dentro da pasta `src/`. Não mexeremos mais na pasta `storefront/assets/`, já que o Webpack se encarregará de colocar os arquivos processados nela.

#### src/assets/

Aqui ficam todos os assets que não são Javascript ou CSS — como imagens e SVGs.

#### src/components/

Nessa pasta moram grande parte dos componentes React.

#### src/editors/

Aqui ficam os componentes que são usados para criar editores: componentes que formam as interfaces que o administrador da loja irá usar para configurar um componente.

#### src/pages/

Os arquivos nesta pasta são componentes React responsáveis por responder por uma rota.

#### src/styles/

Os arquivos LESS ficam dentro dessa pasta.

#### src/utils/

Arquivos Javascript que não se encaixam nas outras pastas.

#### src/my-first-app.jsx

O principal arquivo da aplicação, o ponto de partida de sua app.

#### src/my-first-app-editor.jsx

O arquivo da aplicação voltado para os componentes editores.

#### .eslintrc

Arquivo de configuração do eslint.

#### .gitignore

Arquivo importante caso use git, ferramenta de versionamento de código.

#### .vtexignore

O `.vtexignore` impede que arquivos sejam enviados para a Gallery/Sandbox desnecessariamente. Note que a pasta `src/` está incluida nessa lista, pois esse é o código fonte não processado: o que queremos enviar são apenas os arquivos gerados pelo Webpack, que são arquivos compilados, minificados e otimizados que vão morar dentro da pasta `storefront/assets/`.

#### package.json

Arquivo necessário para projetos Javascript que usam o npm, o package manager de Javascript.

#### webpack.config.js

Esse arquivo possui todas as configurações do Webpack.

### Buildando o código fonte

Para fazer o build do projeto vamos usar o Webpack.

Abra o terminal na pasta de sua app e digite:
```sh
webpack
```

Você pode ver que quatro arquivos foram criados na pasta `storefront/assets/`. Todos eles são códigos Javascript minificados com respectivos *source maps* (arquivos que facilitam debugar o código em ferramentas como o Chrome Developer Tools). Perceba que mesmo tendo arquivos LESS no código fonte, nos arquivos gerados existem apenas arquivos Javascript. O Webpack coloca todo o código CSS dentro do Javascript para se alavancar do cache do browser. Ele também se encarrega de inserir o CSS no código HTML, fazendo com que tudo funcione normalmente.

Agora que temos os arquivos dentro da pasta `storefront/assets/`, podemos enviá-los para a sandbox.

Digite no terminal:
```sh
vtex watch nomedasandbox
```

Confira tudo funcionando no browser.

### Toolbelt para o resgate

Ganhamos a facilidade de escrever em ES7, JSX, LESS, minificar, etc, mas agora temos dois processos rodando, o watch do Toolbelt e o Webpack. Pensando em facilitar ainda mais o desenvolvimento, o Toobelt possui uma opção para quem usa Webpack.

Abra o terminal na pasta de sua app e digite:
```sh
vtex watch nomedasandbox --webpack
```

Dessa forma, o Toolbelt se encarrega de rodar o Webpack e fazer o upload dos arquivos.

### Mais rápido! Mais rápido!

Ainda não estamos rápido o suficiente, vamos usar um dos grandes diferenciais do combo Webpack+React, o hot-loader.

Pare o Toolbelt que está rodando e ligue o novamente com a flag `--server`:
```
vtex watch nomedasandbox --server
```

Essa opção liga um servidor local, o Webpack Dev Server, com ele é possível utilizar o hot-loader. Normalmente quando desenvolvemos em servidores locais acessamos URLs como `http://localhost:3000/`, no nosso caso, vamos usar a URL:

[http://basedevmkp.local.myvtex.com:3000/](http://basedevmkp.local.myvtex.com:3000/)

Faça uma alteração no componente `HomePage.jsx` ou em um arquivo CSS e veja ele realizar as mudanças sem dar reload na página.

## Criando uma nova página

Abra o arquivo `storefront/components/HomePage.json`. Esse arquivo fala para o servidor as seguintes informações:

- **route**: O componente com nome "HomePage" da sua app (nesse caso "alphateam.my-first-app") irá atender o path `/` e ela será identificada no código como "home"
- **assets**: Para que essa página funcione, os arquivos listados nessa propriedade devem estar inseridas na página, e o servidor se encarregará de inserir os arquivos no HTML quando o usuário entrar nessa página

Vamos agora criar um novo arquivo na pasta `storefront/components`, dê o nome de "ProductPage.json" e coloque o seguinte JSON:

```json
{
  "route": {
    "name": "product",
    "path": "/:slug/p"
  },
  "assets": [
    "my-first-app.js"
  ]
}
```

Estamos criando uma página chamada "product", ela será aberta quando o usuário digitar algo como "/short-balneario/p", note a notação ":slug", significa que esse valor é variável.

A propriedade `assets` usa o mesmo arquivo que a "HomePage" pois o Webpack faz o build de toda a aplicação em um único arquivo.

Entre na URL:

[http://basedevmkp.local.myvtex.com:3000/short-balneario/p](http://basedevmkp.local.myvtex.com:3000/short-balneario/p)

Veja que a página está em branco. Isso acontece pois ainda não escrevemos um componente React para atender a essa rota, vamos cria-lo agora.

Crie o arquivo `ProductPage.jsx` na pasta `src/pages/`, com o seguinte código:

```js
import React from 'react';

class ProductPage extends React.Component {
  render() {
    return (
      <h1>Essa é a página de produto!</h1>
    );
  }
}

export default ProductPage;

```

Nada deve acontecer. Isso acontece, pois nosso arquivo principal `src/my-first-app.jsx` não está importando o componente "ProductPage". Abra o arquivo `src/my-first-app.jsx` e substitua o conteúdo pelo seguinte código:

```js
// Importando componentes que respondem por uma página
import HomePage from 'pages/HomePage';
import ProductPage from 'pages/ProductPage';
// Importando dispatcher do SDK
import { dispatcher } from 'sdk';

let components = [
  {
    name: 'HomePage@vtex.my-first-app',
    constructor: HomePage
  },
  {
    name: 'ProductPage@vtex.my-first-app',
    constructor: ProductPage
  }
];

// Chamando action que registra os componentes
dispatcher.actions.ComponentActions.register(components);

// Não preste atenção nisso, é algo que temos que colocar para o hot loader funcionar
// Enable react hot loading with external React
// see https://github.com/gaearon/react-hot-loader/tree/master/docs#usage-with-external-react
if (module.hot) {
  window.RootInstanceProvider = require('react-hot-loader/Injection').RootInstanceProvider;
}

```

```js
// Importando componentes que respondem por uma página
import HomePage from 'pages/HomePage';
import ProductPage from 'pages/ProductPage';
```

Primeiro, importamos os componentes de página usando a sintaxe da versão ES6 do Javascript. O componente é importado de "pages/ProductPage" e seu construtor é inserido na variável `ProductPage`.

```js
// Importando dispatcher do SDK
import { dispatcher } from 'sdk';
```

Depois pegamos apenas a variável `dispatcher` da biblioteca SDK. Essa variável guarda o *dispatcher*, um objeto conceituado pelo [Flux](https://facebook.github.io/flux/docs/overview.html#structure-and-data-flow).

---

### Uma rápida explicação sobre Flux em 30 segundos

O Flux é uma arquitetura que define como os dados são transmitidos por toda a aplicação.

![Flux](https://facebook.github.io/flux/img/flux-simple-f8-diagram-with-client-action-1300w.png)

A View representa os componentes React. O dispatcher é a unidade centralizadora: ele liga as actions às stores. As stores são onde os dados estão armazenados, e os componentes podem ouvir mudanças de uma store. As actions fornecem funções que os componentes podem chamar, fazendo com que os dados das stores mudem. Atenção: as funções das actions não retornam resultados, elas apenas fazem com que as stores mudem e, como os componentes escutam as mudanças das stores, os componentes pegam esses novos dados.

---

```js
let components = [
  {
    name: 'HomePage@vtex.my-first-app',
    constructor: HomePage
  },
  {
    name: 'ProductPage@vtex.my-first-app',
    constructor: ProductPage
  }
];

// Chamando action que registra os componentes
dispatcher.actions.ComponentActions.register(components);
```

Estamos chamando a action `register` da "ComponentActions". Essa action faz com que os componentes sejam registrados na "ComponentStore". Ao registrar os componentes, o SDK consegue pegar o componente na store e, quando a rota do componente é aberta, ele renderiza o componente associado.

Atualize a página do browser para ver as modificações (o hot loader funciona apenas para alterações em componentes React). Você deve agora ver a página de produto!

### Recapitulando

Para criar uma nova página você precisa:

- Criar um arquivo JSON com o nome do componente React que irá responder pela rota em `storefront/components/`
- Criar um componente React em `src/pages/`
- Registrar o componente React na "ComponentStore" utilizando a action "ComponentActions.register"

## Pegando dados do servidor


## Indo além

### Editors
