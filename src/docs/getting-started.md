# Getting Started

## Setup

Para começar, instale o [node](https://gist.github.com/brenoc/534729c806dc0d4ca917) em sua máquina.

Abra o terminal e instale alguns pacotes que serão úteis nesse guia:

```sh
npm install -g yo generator-vtex
npm install -g vtex
```

Caso de erro na instalação, use `sudo`.

Os pacotes yo ([Yeoman](http://yeoman.io/)) e [generator-vtex](https://github.com/vtex/generator-vtex/) são pacotes que geram a estrutura de pastas de apps automaticamente.

Já o pacote `vtex`, é uma ferramenta que chamamos de [Toolbelt](https://github.com/vtex/toolbelt), ela é essencial para o desenvolvimento de apps. Com ela você pode publicar apps na Gallery e desenvolver apps localmente.

Instale também alguma extensão de edição de cookies no browser, caso esteja usando o Google Chrome, recomendamos a [Cookie Inspector](https://chrome.google.com/webstore/detail/cookie-inspector/jgbbilmfbammlbbhmmgaagdkbkepnijn?utm_source=chrome-app-launcher-info-dialog).

## Criando a primeira app

Vamos criar nossa primeira app no Storefront. Crie uma pasta com o nome "my-first-app" e abra o terminal nela.

Rode o seguinte comando para iniciar o `generator-vtex`:
```sh
yo vtex:storefront --simple
```

De o nome de sua primeira app como "my-first-app" e use "alphateam" como vendor.

Algumas pastas e arquivos devem ter sido criados. Vamos entrar mais a fundo na próxima sessão.

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

Nessa pasta moram as definições de componentes usadas pelo servidor do Storefront. Entraremos em detalhes mais a frente.

### resources/

Esses arquivos definem chamadas a APIs, usaremos os recursos em arquivos de componentes e no código Javascript. Entraremos em detalhes mais a frente.

### meta.json

Todas as apps na Gallery precisam do arquivo `meta.json`. Nele ficam registrado diversas informações sobre sua app como o nome (`name`), nome amigável (`title`), descrição (`description`), depedências de outras apps (`dependencies`) e quais serviços são usados (`schemas`).

### .vtexignore

Esse arquivo é usado pelo Toolbelt. Aqui estão listados quais arquivos e pastas não devem ser enviados para a Gallery.

## Workspace e Sandbox

Precisamos de duas coisas para criar um ambiente de desenvolvimento: um workspace próprio e uma sandbox.

### Workspace

Uma loja guarda algumas configurações como, por exemplo, quais apps estão instaladas e qual imagem deve aparecer no banner da home. Esse conjunto de configurações ficam em um workspace. O workspace de produção se chama `master`. Para fazer uma alteração no workspace de produção, você precisa fazer as alterações em um novo workspace e, em seguida, promover esse workspace para `master`.

Para desenvolvermos nossa primeira app, precisamos criar um novo workspace. Vá até:

[http://basedevmkp.vtexcommercebeta.com.br/admin/gallery#/workspaces](http://basedevmkp.vtexcommercebeta.com.br/admin/gallery#/workspaces)

Clique em "Novo workspace" e crie um workspace com o seu nome.

### Sandbox

É um ambiente de desenvolvimento de apps. Para entender o como uma sandbox funciona, devemos entender como a Gallery funciona.

- Usuário abre uma página da loja
- Servidor verifica quais apps estão instaladas
- Servidor processa os arquivos das apps que estão armazenadas na Gallery
- Servidor responde a página para o usuário

Quando o desenvolvedor usa uma sandbox, o que acontece é o seguinte:

- Usuário abre uma página da loja
- **Servidor verifica quais apps estão na sandbox**
- **Servidor processsa os arquivos das apps que estão armazenadas na Sandbox**
- Servidor verifica quais apps estão instaladas
- Servidor processa os arquivos das apps que estão armazenadas na Gallery
- Servidor responde a página para o usuário

A sandbox cria uma espécie de Gallery temporária e privada para facilitar o desenvolvimento de apps. Sem ela, o desenvolvedor teria que lançar uma versão nova de sua app na Gallery, instalar a app e, só assim, ver as mudanças. Ou seja, sandbox é ótima e ela será sua nova amiga!

### Ativando o workspace e sandbox

Para ativar o workspace e sua sandbox você deve criar alguns cookies.

Primeiro, entre na URL da loja no ambiente de desenvolvimento:

[http://basedevmkp.beta.myvtex.com/](http://basedevmkp.beta.myvtex.com/)

Caso você tenha instalado a extensão [Cookie Inspector](https://chrome.google.com/webstore/detail/cookie-inspector/jgbbilmfbammlbbhmmgaagdkbkepnijn?utm_source=chrome-app-launcher-info-dialog) sugerida, abra o Developer Tools do Chrome (F12 ou Command+Option+i) e clique na aba "Cookies", clique com o botão direito do mouse e, em seguida, "Add new cookie".

Crie o cookie do workspace:

Nome|Valor
---|---
vtex_workspace|nomedomeuworkspace

Para criar o cookie da sandbox, vamos precisar de:

- Nome do `vendor` da app. Nesse caso usamos "alphateam"
- Nome da sua sandbox. Fique a vontade pra escolher (ele deve ser único!)
- Nome da sua app. Nesse caso usamos "my-first-app"

O formato do cookie:

Nome|Valor
---|---
vtex_sandbox|nomedovendor/nomedasandbox=nomedaapp

Logo, deve ficar algo assim (certifique-se de colocar o nome da sua sandbox):

Nome|Valor
---|---
vtex_sandbox|alphateam/nomedasandbox=my-first-app

## Hello World!

Agora que temos tudo pronto para por a mão na massa, vamos ver o tão esperado "Hello World!".

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

- Leu o arquivo `meta.json` e viu o vendor e o nome da sua app
- Leu o arquivo `.vtexignore` e guardou quais arquivos ela não deve fazer upload
- Fez o upload de todos arquivos que não estão na lista de arquivos do `.vtexignore`

Esses arquivos vão parar dentro da pasta "alphateam.my-first-app", que é o identificador único de uma app, dentro da sua sandbox.

Abra a URL da loja em desenvolvimento:

[http://basedevmkp.beta.myvtex.com/](http://basedevmkp.beta.myvtex.com/)

Você deve estar vendo "Hello World!" escrito na tela.

O Toolbelt está escutando qualquer modificação feita nos arquivos de sua app. Podemos testar isso abrindo o arquivo `assets/index.js` e alterando o texto "Hello World!". Salve o arquivo. Verá que o Toolbelt fez o upload para a sandbox. Note também que a página deu refresh, isso acontece automaticamente por conta do sistema de livereload.

## Melhorando o processo de desenvolvimento

Apesar de funcionar bem, essa forma de desenvolvimento pode se tornar tediosa a medida que sua app começa a crescer. Arquivos Javascript e CSS começam a se proliferar e escrever React sem JSX é bem estranho. Além disso, nosso código não está minificado e não estamos usando nenhum pré-processador de CSS, como LESS ou SASS.

Para resolver tudo isso, vamos colocar uma ferramenta de build. Hoje, no meio Javascript, existem diversas alternativas: Grunt, Gulp, Webpack, Browserify, etc. Aqui no VTEX Lab já testamos todas essas e acabamos preferindo o Webpack, principalmente para projetos React. Um grande diferencial é o `react-hot-loader`, ele é uma espécie de livereload 2.0, a diferença é que ao invés de recarregar a página (o que as vezes demora), ele apenas recarrega o componente React que foi modificado fazendo com que o ciclo de desenvolvimento fique *muito* mais rápido.

Acabamos construindo uma estrutura de desenvolvimento opinionada baseada em Webpack, LESS, ES7 e eslint. ES7 é a mais recente versão do Javascript que será lançada em 2016, então já estamos escrevendo mirando para o futuro. Mas não esquecemos do IE8! Usamos o Babel, uma ferramenta que transforma o código ES7 para a versão atual do Javascript. eslint é uma ferramenta que padroniza como o código deve ser escrito. LESS é o pré-processador CSS escolhido pelo VTEX Lab, também um dos mais usados pela comunidade front-end. Por fim, o Webpack, que faz tudo isso funcionar como mágica, além de minificar imagens, SVGs, Javascript e CSS.

Não se apague ao seu app agora, vamos apagar todo o seu conteúdo e começa-lo do zero com essa nova estrutura de desenvolvimento.

Apague todos os arquivos da pasta de sua app. Abra o terminal na mesma pasta e digite:

```sh
yo vtex:storefront
```

Crie a app com o nome "my-first-app", e "alphateam" como vendor.

Verá que algumas pastas e arquivos devem ter sido criados e as dependências node foram instaladas.

### Nova estrutura de pastas

Agora sua app deve parecer com isso:

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

Nessa nova estrutura, escreveremos a maior parte do nosso código dentro da pasta `src/`. Não mexeremos mais na pasta `storefront/assets/`, o Webpack se encarregará de colocar os arquivos compilados nela.

#### src/assets/

Aqui ficam todos os assets que não são Javascript, nem CSS, como imagens e SVGs.

#### src/components/

Nessa pasta moram grande parte dos componentes React.

#### src/editors/

Aqui ficam os componentes que são usados para criar editores, componentes que o administrador da loja irá usar para editar um componente.

#### src/pages/

Os arquivos aqui são componentes React responsáveis por responder por uma rota.

#### src/styles/

Os arquivos LESS ficam dentro dessa pasta.

#### src/utils/

Aqui ficam arquivos Javascript que não se encaixam nas outras pastas.

#### src/my-first-app.jsx

Esse é o arquivo principal da aplicação.

#### src/my-first-app-editor.jsx

Esse é o arquivo da aplicação voltado para os componentes editores.

#### .eslintrc

Arquivo de configuração do eslint.

#### .gitignore

Arquivo importante caso use git, ferramenta de versionamento de código.

#### .vtexignore

O `.vtexignore` impede que arquivos sejam enviados para a Gallery/Sandbox desnecessariamente. Note que a pasta `src/` está incluida nessa lista, pois esse é o código fonte não processado, o que queremos enviar são apenas os arquivos gerados pelo Webpack, que são arquivos compilados, minificados e otimizados que vão morar dentro da pasta `storefront/assets/`.

#### package.json

Arquivo necessário para projetos Javascript que usam o npm, o package manager de Javascript.

#### webpack.config.js

Esse arquivo possui todas as configurações do Webpack.

### React com JSX

### Como adicionar arquivos LESS

### Como usar imagens

## Usando o SDK

### Apresentando o Flux

### Registrando componentes

### Stores do SDK

### Pegando dados das stores

## Indo além

### Editors
