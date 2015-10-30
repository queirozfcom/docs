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

---

Até então, as coisas não estão funcionando! Agora que temos tudo pronto para pôr a mão na massa, vamos ver o tão esperado "Hello World!".

## Hello World!

Vamos subir a nossa app na Gallery. Abra o terminal na pasta da app e digite:

```sh
vtex watch
```

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

O Toolbelt está escutando qualquer modificação feita nos arquivos de sua app. Podemos testar isso abrindo o arquivo `assets/index.js` e alterando o texto "Hello World!". Salve o arquivo. Verá que o Toolbelt fez o upload para a Gallery. Note também que a página deu refresh, isso acontece automaticamente por conta do sistema de livereload.

---

Você completou o "Primeiros Passos"! Você já sabe utilizar as ferramentas e está pronto para dar o próximo passo.

Próximo passo: [Melhorando o processo de desenvolvimento](2-melhorando-o-processo-de-desenvolvimento.md)
