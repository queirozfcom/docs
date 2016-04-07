# Setup

Para desenvolver apps na VTEX você precisará instalar o node, npm e o VTEX Toolbelt.

## Node.js

O Storefront usa diversas ferramentas desenvolvidas em Node.js (ou Node), por isso é essencial que o tenha instalado no computador. O Node.js é uma runtime de desenvolvimento baseada em Javascript. Saiba mais sobre o Node em sua [página oficial](https://nodejs.org/).

[Instruções de como instalar o node.](https://gist.github.com/brenoc/534729c806dc0d4ca917)

### VTEX Toolbelt

O pacote Node `vtex` é uma ferramenta que chamamos de [Toolbelt](https://github.com/vtex/toolbelt).

O Toolbelt é essencial para o desenvolvimento de apps, pois permite que você desenvolva seu app localmente vendo mudanças no browser em tempo real, além de publicar seus apps na Gallery quando estiverem prontas para ir para produção.

```sh
npm install -g vtex@beta
```

Verifique se o Toolbelt foi instalado corretamente digitando:

```sh
vtex
```

Caso encontre algum erro durante a instalação, leia: [Solução de erros comuns durante a instalação de pacotes node](../solucao-de-problemas.md)

---

## Algumas recomendações

As ferramentas abaixo não são obrigatórias, mas acreditamos que elas facilitem o desenvolvimento.

## Ferramentas para o Windows

Caso use o Windows, é recomendado a instalação do [Git Bash](https://git-for-windows.github.io/) e do [ConEmu](https://conemu.github.io/), já que eles melhoram a experiência de uso de linha de comando. Depois de instalar o ConEmu, configure-o para usar o Git Bash ([instruções](https://gist.github.com/brenoc/fb704b6217fa24e26c97)).

## Atom

Recomendamos o uso do editor de texto open-source [Atom](http://atom.io) para o desenvolvimento, mas caso prefira usar o Sublime ou outro editor de texto, não há problema.

### Pacotes Atom

O Atom oferece um repositório oficial de pacotes que aumentam suas funcionalidades. Para instalar os pacotes que usamos para desenvolvimento no Storefront, Abra o terminal e digite:

```sh
apm install language-babel linter linter-eslint
```

### Configurando o Atom

Abra `Settings > Packages` e procure por "language-babel" e clique no botão "Settings". Desmarque a checkbox "Transpile on save". Ao fechar a aba de Settings, as configurações serão salvas automaticamente.


## Sublime Text

Caso prefira usar o [Sublime Text](http://www.sublimetext.com/) em seu Workflow, sem problemas. Também podemos facilitar sua vida instalando alguns packages.

> As instruções abaixo levam em conta que você possui o [Package Control](https://packagecontrol.io/) instalado em seu editor.

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

Você completou o setup inicial do Storefront. Agora estamos prontos para por mão na massa! Comece o seu app [definindo um manifest](manifest.md).
