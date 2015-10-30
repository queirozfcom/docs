# Primeiros Passos

## Criando a primeira app

Vamos criar nossa primeira app no Storefront. Crie uma pasta com o nome "my-first-app" e abra o terminal nela.

Rode o `generator-vtex` com o seguinte comando:
```sh
yo vtex:storefront --simple
```

E responda as perguntas com:

- Dê o nome de "my-first-app"
- Digite "alphateam" como vendor

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

Vá até [o admin de workspaces](http://basedevmkp.vtexcommercebeta.com.br/admin/gallery#/workspaces), clique em "Novo workspace" e crie um workspace com o seu nome todo em letras minúsculas, sem espaços ou acentuações.

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

Para ativar o workspace e sua sandbox você não precisa fazer **nada**. Não, não é uma pegadinha!

Quando você usa o comando necessário para observar seus arquivos e mandá-los para o servidor, fazemos diversas inferências baseados nos seus dados de login e a única coisa que você precisa fazer é clicar/copiar uma URL que o Toolbelt mostra pra você quando termina de enviar seus arquivos.

---

Até então, as coisas não estão funcionando! Agora que temos tudo pronto para pôr a mão na massa, vamos ver o tão esperado "Hello World!".

## Hello World!

Vamos subir a nossa app na sandbox. Abra o terminal na pasta da app e digite:

```sh
vtex watch
```

Note que ao rodar o comando ele irá pedir que você faça um login. Isso é necessário para que possamos enviar os arquivos para a Gallery. Não se preocupe, uma vez logado seu acesso tem duração de 24 horas.

Ao fazer o login, use `basedevmkp` como account e prossiga com suas credenciais da VTEX posteriormente.

Após fazer o login, verá que o Toolbelt mostrará uma linda mensagem e algo assim:

```
Watching nomedasuaapp

U meta.json
U storefront/assets/index.js
U storefront/components/HomePage.json

... files uploaded

Your URL: http://basedevmkp.beta.myvtex.com/?workspace=sb_seuemail
```

O que o Toolbelt acabou de fazer foi:

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
