# Setup Inicial

Para começar a desenvolver para o Storefront é necessário que tenha uma noção básica de React e que seu ambiente de desenvolvimento tenha alguns pacotes node instalados.

Para ter uma boa introdução ao React, recomendamos fazer o [tutorial oficial](http://facebook.github.io/react/docs/tutorial.html). É bem divertido!

Você precisará instalar:

 - [Node.js](#nodejs)
 - [Pacotes Node](#pacotes-node)
 - [Yeoman](#yeoman)
 - [Generator VTEX](#generator-vtex)
 - [VTEX Toolbelt](#vtex-toolbelt)


 - [Configurações específicas para Windows](#configurações-para-windows)
 - [Atom (Opcional)](#atom-opcional)
 - [Sublime Text (Opcional)](#sublime-text-opcional)

---

## Node.js

O Storefront usa diversas ferramentas desenvolvidas em Node.js (ou Node), por isso é essencial que o tenha instalado no computador. O Node.JS é uma runtime de desenvolvimento baseada em Javascript. Saiba mais sobre o Node em sua [página oficial](https://nodejs.org/).

[Instruções de como instalar o node.](https://gist.github.com/brenoc/534729c806dc0d4ca917)

## Pacotes Node

Vamos instalar alguns pacotes Node que usaremos para desenvolver apps no Storefront. Esses pacotes são disponibilizados pelo [NPM](https://www.npmjs.com/) (Node Package Manager).

Caso encontre algum erro durante a instalação de pacotes do Node, leia: [Solução de erros comuns durante a instalação de pacotes node](https://github.com/vtex-apps/docs/blob/refactor/new-docs/1_guias/solucao-de-erros-comuns-durante-a-instalacao-de-pacotes-node.md)

### Yeoman

O pacote yo ([Yeoman](http://yeoman.io/)) é uma ferramenta que permite criar e rodar geradores de estrutura de pastas e código, como o Generator VTEX. Para instalar:

```sh
npm install -g yo
```

Verifique se o pacote yo (chamado de Yeoman) foi instalado corretamente digitando:

```sh
yo
```

### Generator VTEX

O [generator-vtex](https://github.com/vtex/generator-vtex/) é um gerador de estrutura de pastas para apps VTEX. Ao rodar o Generator você terá toda a estrutura básica necessária para começar a desenvolver seu app.

```sh
npm install -g generator-vtex
```

Verifique se o pacote generator-vtex foi instalado corretamente digitando:

```sh
yo vtex
```

### VTEX Toolbelt

O pacote `vtex` é uma ferramenta que chamamos de [Toolbelt](https://github.com/vtex/toolbelt).

O Toolbelt é essencial para o desenvolvimento de apps, pois permite que você desenvolva seu app localmente vendo mudanças no browser em tempo real, além de publicar seus apps na Gallery quando estiverem prontas para ir para produção.

```sh
npm install -g vtex
```

Verifique se o Toolbelt foi instalado corretamente digitando:

```sh
vtex
```

---

### Configurações para Windows

Caso use o Windows, instale o [Git Bash](https://git-for-windows.github.io/) e o [ConEmu](https://conemu.github.io/), eles facilitam o uso do terminal. Depois configure o ConEmu para usar o Git Bash ([instruções](https://gist.github.com/brenoc/fb704b6217fa24e26c97)).

## Atom (opcional)

Recomendamos o uso do editor de texto open-source [Atom](http://atom.io) para o desenvolvimento, mas caso prefira usar o Sublime ou outro editor de texto, não há problema.

### Pacotes Atom

O Atom oferece um repositório oficial de pacotes que aumentam suas funcionalidades. Para instalar os pacotes que usamos para desenvolvimento no Storefront, Abra o terminal e digite:

```sh
apm install language-babel linter linter-eslint
```

### Configurando o Atom

Abra `Settings > Packages` e procure por "language-babel" e clique no botão "Settings". Desmarque a checkbox "Transpile on save" e no campo "Babel stage" digite "0". Ao fechar a aba de Settings, as configurações serão salvas automaticamente.

---

## Sublime Text (opcional)

Caso prefira usar o [Sublime Text](http://www.sublimetext.com/) em seu Workflow, sem problemas. Também podemos facilitar sua vida instalando alguns packages.

### Pacotes Sublime

Abra a tela de comandos digitando `cmd+shift+p` no Mac OS X, ou `ctrl+shift+p` no Linux/Window. Depois digite:

```sh
Package Control: Install Package
```
E procure pelos pacotes:

```sh
Babel SublimeLinter SublimeLinter-contrib-eslint
```

---

### Próximos Passos

Você completou o Setup inicial do Storefront. Agora você já pode colocar a mão na massa e começar uma app do zero ou customizar uma já existente.

Saiba mais sobre o [ambiente de desenvolvimento](4-ambiente-de-desenvolvimento.md) do Storefront, veja nosso [Tutorial](2-criando-seu-primeiro-app.md) para aprender a desenvolver um app básico ou cheque nossos guias para necessidades mais específicas.

Caso busque informações sobre uso avançado do Storefront, veja [a documentação de nosso SDK](http://vtex-apps.github.io/storefront-sdk/).
