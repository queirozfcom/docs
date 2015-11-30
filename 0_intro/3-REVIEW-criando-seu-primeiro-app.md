# Criando sua Primeira App

Vamos criar nossa primeira app no Storefront. Crie uma pasta com o nome "my-first-app" e abra o terminal nela.

Rode o `generator-vtex` com o seguinte comando:
```sh
yo vtex:storefront --simple
```

E responda as perguntas com:

- Dê o nome de "nomedoseuapp"
- Digite "alphateam" como vendor

Em algumas instalações do node, o comando acima pode dar erro. Se tiver problemas, rode o comando com `sudo`.

Este processo irá criar a estrutura de pastas e arquivos iniciais de seu App.

## Estrutura de pastas

Um App no Storefront tem as seguintes pastas e arquivos:

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

Todas os Apps na Gallery precisam do arquivo `meta.json`. Nele ficam registradas diversas informações sobre seu App como o nome (`name`), nome amigável (`title`), descrição (`description`) e depedências de outros Apps (`dependencies`).

### .vtexignore

Esse arquivo é usado pelo Toolbelt. Aqui estão listados quais arquivos e pastas não devem ser enviados para a Gallery. Caso seja familiar com o git, ele funciona da mesma forma que o `.gitignore`.

---

Até então, as coisas não estão funcionando! Agora que temos tudo pronto para pôr a mão na massa, vamos ver o tão esperado "Hello World!".

## Hello World!

Vamos subir nosso App na Gallery. Abra o terminal na pasta do App e digite:

```sh
vtex watch
```

Note que ao rodar o comando ele irá pedir que você faça um login. Isso é necessário para que possamos enviar os arquivos para a Gallery. Não se preocupe, uma vez logado seu acesso tem duração de 24 horas.

Ao fazer o login, use `basedevmkp` como account e prossiga com suas credenciais da VTEX posteriormente.

Após fazer o login, verá que o Toolbelt mostrará uma linda mensagem e algo assim:

```
Watching nomedoseuapp

U meta.json
U storefront/assets/index.js
U storefront/components/HomePage.json

... files uploaded

Your URL: http://sualoja.beta.myvtex.com/?workspace=sb_seuemail
```

O que o Toolbelt acabou de fazer foi:

- Ler do arquivo `meta.json`, o nome e o vendor de seu App
- Ler o arquivo `.vtexignore` e guardar quais arquivos ela não deve fazer upload
- Upload de todos os arquivos que não estão na lista de arquivos do `.vtexignore`

Abra a URL da loja em desenvolvimento clicando ou copiando o link disponibilizado pelo Toolbelt.

Você deve estar vendo "Hello World!" escrito na tela.

O Toolbelt está escutando qualquer modificação feita nos arquivos de seu App. Podemos testar isso abrindo o arquivo `assets/index.js` e alterando o texto "Hello World!". Salve o arquivo. Verá que o Toolbelt fez o upload para a Gallery. Note também que a página deu refresh, isso acontece automaticamente por conta do sistema de livereload.
