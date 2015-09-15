# Primeiros Passos

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

Para isso e para ver suas alterações, é necessário criar um cookie específico em seu browser. Para facilitar este processo, instale alguma extensão de edição de cookies no browser.

Caso esteja usando o Google Chrome, recomendamos a [Cookie Inspector](https://chrome.google.com/webstore/detail/cookie-inspector/jgbbilmfbammlbbhmmgaagdkbkepnijn?utm_source=chrome-app-launcher-info-dialog).

## Criando a primeira app

Vamos criar nossa primeira app no Storefront. Crie uma pasta com o nome "my-first-app" e abra o terminal nela.

Rode o `generator-vtex`, o responda com:

- Dê o nome de "my-first-app"
- Digite "alphateam" como vendor

Use o seguinte comando para iniciá-lo:
```sh
yo vtex:storefront --simple
```

Em algumas instalações do node, o comando acima pode dar erro. Se tiver problemas, rode o comando com `sudo`.

Este processo irá criar a estrutura de pastas e arquivos iniciais de sua App.

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

Nessa pasta moram as definições de componentes usadas pelo servidor do Storefront.

### resources/

Esses arquivos definem chamadas a APIs, usaremos os recursos em arquivos de componentes e no código Javascript.

### meta.json

Todas as apps na Gallery precisam do arquivo `meta.json`. Nele ficam registradas diversas informações sobre sua app como o nome (`name`), nome amigável (`title`), descrição (`description`) e depedências de outras apps (`dependencies`).

### .vtexignore

Esse arquivo é usado pelo Toolbelt. Aqui estão listados quais arquivos e pastas não devem ser enviados para a Gallery. Caso seja familiar com o git, ele funciona da mesma forma que o `.gitignore`.

## Workspaces e Sandbox

Precisamos de duas coisas para criar um ambiente de desenvolvimento: um workspace próprio e uma sandbox.

### Workspace

Uma loja possui diversas configurações: quais apps estão instaladas e qual imagem deve aparecer no banner da home, por exemplo. Este conjunto de configurações fica guardada em um workspace. O workspace de produção chama-se `master`. Para fazer uma alteração no workspace de produção, é preciso fazer as alterações em um novo workspace e, em seguida, promover esse workspace para `master`.

Para desenvolvermos nossa primeira app, precisaremos criar um novo workspace.

Vá até [o admin de workspaces](http://basedevmkp.vtexcommercebeta.com.br/admin/gallery#/workspaces), clique em "Novo workspace" e crie um workspace com o seu nome.

### Sandbox

A Sandbox é um ambiente de desenvolvimento de apps. Para entender como funciona, devemos entender primeiro como a Gallery funciona.

Este é o fluxo de dados de uma loja no StoreFront:

1. Usuário abre uma página da loja
2. Servidor verifica quais apps estão instaladas
3. Servidor processa os arquivos das apps que estão armazenadas na Gallery
4. Servidor responde com a página para o usuário

A sandbox cria uma espécie de Gallery temporária e privada para facilitar o desenvolvimento de apps. Sem ela, um desenvolvedor teria que lançar uma versão nova de sua app na Gallery e instalar a app para ver as mudanças.

Quando o desenvolvedor usa uma sandbox, o fluxo é o seguinte:

1. Usuário abre uma página da loja  
1.1 **Servidor verifica quais apps estão na sandbox**  
1.2 **Servidor processsa os arquivos das apps que estão armazenadas na Sandbox**  
2. Servidor verifica quais apps estão instaladas
3. Servidor processa os arquivos das apps que estão armazenadas na Gallery
4. Servidor responde a página para o usuário

A sandbox é ótima! Ela será sua nova amiga :)

### Ativando o workspace e a sandbox

Para ativar o workspace e sua sandbox você deve adicionar dois cookies em seu browser. Isso é necessário para que o servidor verifique qual é a sua sandbox e quais apps estão sendo desenvolvidos nela.

Primeiro, entre na URL da loja no ambiente de desenvolvimento:

[http://basedevmkp.beta.myvtex.com/](http://basedevmkp.beta.myvtex.com/)

Caso você tenha instalado a extensão [Cookie Inspector](https://chrome.google.com/webstore/detail/cookie-inspector/jgbbilmfbammlbbhmmgaagdkbkepnijn?utm_source=chrome-app-launcher-info-dialog), abra o Developer Tools do Chrome (`F12` ou `command+option+i`), escolha a aba "Cookies", clique com o botão direito do mouse e em seguida, "Add new cookie".

Vamos criar dois cookies, um para o workspace e outro para a sandbox.

#### Criando o cookie do workspace

Crie o cookie do workspace.

Nome|Valor
---|---
vtex_workspace|nomedomeuworkspace

Lembre-se que:

- Os cookies devem ser editados na página: [http://basedevmkp.beta.myvtex.com/](http://basedevmkp.beta.myvtex.com/)
- O workspace deve ser criado:

> Vá até [o admin de workspaces](http://basedevmkp.vtexcommercebeta.com.br/admin/gallery#/workspaces), clique em "Novo workspace" e crie um workspace com o seu nome.


#### Criando o cookie da sandbox

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

Até então, as coisas não estão funcionando! Agora que temos tudo pronto para pôr a mão na massa, vamos ver o tão esperado "Hello World!".

## Hello World!

Vamos subir a nossa app na sandbox. Abra o terminal na pasta da app e digite:

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

- Ler do arquivo `meta.json`, o nome e o vendor de sua app
- Ler o arquivo `.vtexignore` e guardar quais arquivos ela não deve fazer upload
- Upload de todos os arquivos que não estão na lista de arquivos do `.vtexignore`

Estes arquivos vão parar dentro da pasta "alphateam.my-first-app", que é o identificador único de uma app dentro da sua sandbox.

Abra a URL da loja em desenvolvimento:

[http://basedevmkp.beta.myvtex.com/](http://basedevmkp.beta.myvtex.com/)

Você deve estar vendo "Hello World!" escrito na tela.

O Toolbelt está escutando qualquer modificação feita nos arquivos de sua app. Podemos testar isso abrindo o arquivo `assets/index.js` e alterando o texto "Hello World!". Salve o arquivo. Verá que o Toolbelt fez o upload para a sandbox. Note também que a página deu refresh, isso acontece automaticamente por conta do sistema de livereload.

---

Você completou o "Primeiros Passos"! Você já sabe utilizar as ferramentas e está pronto para dar o próximo passo.

Próximo passo: [Melhorando o processo de desenvolvimento](2-melhorando-o-processo-de-desenvolvimento.md)
