# Setup

Para o Alpha precisamos que você tenha alguma noção básica de React e que o computador tenha algumas coisas instaladas.

## React

Para ter uma boa introdução ao React, recomendamos fazer o [tutorial oficial](http://facebook.github.io/react/docs/tutorial.html). É bem divertido!

## Node

Vamos usar diversas ferramentas desenvolvidas em node, para isso, e essencial que o tenha instalado no computador.

[Instruções de como instalar o node.](https://gist.github.com/brenoc/534729c806dc0d4ca917)

### Windows

Caso use o Windows, instale o [Git Bash](https://git-for-windows.github.io/) e o [ConEmu](https://conemu.github.io/), eles facilitam o uso do terminal. Depois configure o ConEmu para usar o Git Bash ([instruções](https://gist.github.com/brenoc/fb704b6217fa24e26c97)).

## Pacotes Node

Vamos instalar alguns pacotes node que usaremos para desenvolver apps no Storefront.

Caso dê algum erro durante a instalação leia: [Solução de erros comuns durante a instalação de pacotes node](solucao-de-erros-comuns-durante-a-instalacao-de-pacotes-node.md)

### Yeoman

```sh
npm install -g yo
```

Verifique se o pacote yo (chamado de Yeoman) foi instalado corretamente digitando:

```sh
yo
```

O pacote yo ([Yeoman](http://yeoman.io/)) é uma ferramenta que facilita a criação de geradores de estrutura de pastas e código, como o Generator VTEX.

### Generator VTEX

```sh
npm install -g generator-vtex
```

Verifique se o pacote generator-vtex foi instalado corretamente digitando:

```sh
yo vtex
```

O [generator-vtex](https://github.com/vtex/generator-vtex/) é um gerador de estrutura de pastas de apps VTEX.

### VTEX Toolbelt

```sh
npm install -g vtex
```

Verifique se o Toolbelt foi instalado corretamente digitando:

```sh
vtex
```

O pacote `vtex` é uma ferramenta que chamamos de [Toolbelt](https://github.com/vtex/toolbelt). O Toolbelt é essencial para o desenvolvimento de apps, pois permite que você publique apps na Gallery e desenvolva localmente.


## Extensão de edição de cookies

Para o desenvolvimento de apps é necessário criar alguns cookies em seu browser. Para facilitar este processo, instale alguma extensão de edição de cookies no browser.

Caso esteja usando o Google Chrome, recomendamos a [Cookie Inspector](https://chrome.google.com/webstore/detail/cookie-inspector/jgbbilmfbammlbbhmmgaagdkbkepnijn?utm_source=chrome-app-launcher-info-dialog).

## Atom (opcional)

Recomendamos o uso do editor de texto open-source [Atom](http://atom.io) para o desenvolvimento. Caso prefira usar o Sublime ou outro editor de texto, tudo bem.

### Pacotes Atom

Instale os pacotes do Atom. Abra o terminal e digite:

```sh
apm install language-babel linter linter-eslint
```

### Configurando o Atom

Abra a Settings > Packages e procure por "language-babel", clique no botão "Settings". Desmarque a checkbox "Transpile on save" e no campo "Babel stage" digite "0", pode fechar a aba, ele salva as configurações automaticamente.

---

Você completou o "Setup"! Agora você está preparado para por a mão na massa!

Próximo passo: [Primeiros passos](1-primeiros-passos.md)
