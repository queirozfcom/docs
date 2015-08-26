# Getting Started

## Setup

Para começar, instale o [node](https://gist.github.com/brenoc/534729c806dc0d4ca917) em sua máquina.

Abra o terminal e instale alguns pacotes que serão úteis nesse guia:

```sh
npm install -g yo generator-vtex
npm install -g vtex
```

Caso de erro na instalação, use `sudo`.

Os pacotes `yo` e `generator-vtex` são pacotes que geram a estrutura de pastas de apps automaticamente.

Já o pacote `vtex`, é uma ferramenta que chamamos de Toolbelt, ela é essencial para o desenvolvimento de apps. Com ela você pode publicar apps na Gallery e desenvolver apps localmente.

Instale também alguma extensão de edição de cookies no browser, caso esteja usando o Google Chrome, recomendamos a [Cookie Inspector](https://chrome.google.com/webstore/detail/cookie-inspector/jgbbilmfbammlbbhmmgaagdkbkepnijn?utm_source=chrome-app-launcher-info-dialog).

## Criando o primeiro app

Vamos criar nosso primeiro app no Storefront. Crie uma pasta com o nome "my-first-app" e abra o terminal nela.

Rode o seguinte comando para iniciar o `generator-vtex`:
```sh
yo vtex:storefront --simple
```

De o nome de seu primeiro app como "my-first-app". Use "alphateam" como vendor.

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

### assets

Aqui ficam todos os arquivos que podem ser acessados publicamente, como arquivos Javascript, CSS, imagens, SVG, fontes, o que quiser.

### components

Nessa pasta moram as definições de componentes usadas pelo servidor do Storefront.

### resources

Esses arquivos definem chamadas a APIs, o servidor do Storefront irá criar novas rotas para acessar essas APIs em `/_resources/:resourceName/`.

### meta.json

Todos apps na Gallery precisam do arquivo `meta.json`. Nele ficam registrado diversas informações sobre seu app como o nome (`name`), nome amigável (`title`), descrição (`description`), depedências de outras apps (`dependencies`) e quais serviços são usados (`schemas`).

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
- Servidor processsa os arquivos das apps que estão armazenados na Gallery
- Servidor responde a página para o usuário

Quando o desenvolvedor usa uma sandbox, o que acontece é o seguinte:

- Usuário abre uma página da loja
- **Servidor verifica quais apps estão na sandbox**
- **Servidor processsa os arquivos das apps que estão armazenadas na Sandbox**
- Servidor verifica quais apps estão instaladas
- Servidor processsa os arquivos das apps que estão armazenados na Gallery
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
- Nome da sua app. Nesse caso usamo "my-first-app"

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
- Fez o upload de todos arquivos na pasta e que não estão na lista de arquivos do `.vtexignore`

Esses arquivos vão parar dentro da pasta "alphateam.my-first-app", que é o identificador único de uma app, dentro da sua sandbox.

Abra a URL da loja em desenvolvimento:

[http://basedevmkp.beta.myvtex.com/](http://basedevmkp.beta.myvtex.com/)

Você deve estar vendo "Hello World!" escrito na tela.

O Toolbelt está escutando qualquer modificação feita nos arquivos de sua app. Podemos testar isso abrindo o arquivo `assets/index.js` e alterando o texto "Hello World!". Salve o arquivo. Verá que o Toolbelt fez o upload para a sandbox. Note também que a página deu refresh, isso acontece automaticamente por conta do sistema de livereload.

## Melhorando o processo de desenvolvimento

```sh
yo vtex:storefront
```

### React com JSX

### Como adicionar arquivos LESS

### Como usar imagens

## Usando o SDK

### Aprensentando o Flux

### Registrando componentes

### Stores do SDK

### Pegando dados das stores

## Indo além

### Editors
