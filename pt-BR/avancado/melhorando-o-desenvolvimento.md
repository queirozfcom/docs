# Melhorando o processo de desenvolvimento

Se você fez o tutorial [Primeiros passos](/primeiros-passos.md), já conhece o fluxo de desenvolvimento básico do Storefront.

Apesar de funcionar bem, essa forma de desenvolvimento pode se tornar tediosa à medida que seu app começa a crescer. Arquivos Javascript e CSS começam a se proliferar e escrever React sem JSX não é ideal. Além disso, nosso código não está minificado e não estamos usando nenhum pré-processador de CSS, como LESS ou Sass.

Para resolver tudo isso, usamos a ferramenta de build [Webpack](https://webpack.github.io/) e uma estrutura de desenvolvimento opinionada que usa ES6 (e até o 7!), eslint, LESS/Sass e react-hot-loader. Em detalhes:

 - ES6 é a mais recente versão do Javascript que foi lançada em 2015, então já estamos escrevendo. Muitos browsers ainda não são compatíveis com ES6, mas não se preocupe! Usamos o Babel, uma ferramenta que transforma o código Javascript ES6 para a versão ES5, compatível com os browsers de hoje.

 - ESlint é uma ferramenta que padroniza como o código deve ser escrito.

 - Você pode escolher entre LESS e Sass como pré-processador CSS para seus componentes.

 - O react-hot-loader é uma espécie de livereload avançado que, ao invés de recarregar toda a página, atualiza apenas o componente React que foi modificado. Isso faz com que o ciclo de desenvolvimento seja **muito** mais rápido.

 - Por fim, o Webpack agrega todas essas ferramentas e faz todas funcionarem como mágica, além de minificar imagens, SVGs, Javascript e CSS.

## Nova estrutura de pastas

Neste guia vamos apagar toda a estrutura criada no Tutorial básico e começá-la do zero com essa nova estrutura de desenvolvimento.

Para os passos a seguir, você deverá instalar os pacotes `yo` e `generator-vtex` (lembrando de usar `sudo` ou equivalente caso seja necessário):

```sh
$ npm install -g yo
$ npm install -g generator-vtex
```

Apague todos os arquivos da pasta de seu app. Abra o terminal na mesma pasta e digite:

```sh
yo vtex:storefront
```

Responda o generator com:
- `my-first-app`
- `nome-da-sua-empresa`
- `yes` (ou `y`)
- `yes` (ou `y`)

Você verá que algumas pastas e arquivos foram criados e as dependências do node foram instaladas. Seu app agora deve parecer com isso:

```
.
├── src/
│   ├── assets/
│   ├── components/
│   ├── editors/
│   └── utils/
├── storefront/
│   ├── assets/
│   ├── components/
│   ├── routes/
|   ├── settings/
|   |   ├── components/
|   |   └── routes/
│   └── resources/
├── .eslintrc
├── .gitignore
├── .vtexignore
├── manifest.json
├── package.json
└── webpack.config.js
```

Nessa nova estrutura, escreveremos a maior parte do nosso código dentro da pasta `src/`. Não mexeremos mais na pasta `storefront/assets/`, já que o Webpack se encarregará de colocar os arquivos processados nela.

## Arquivos de desenvolvimento

#### src/assets/

Aqui ficam todos os assets que não são Javascript ou CSS — como imagens e SVGs.

#### src/components/

Nessa pasta moram todos os componentes React da app.

#### src/editors/

Aqui ficam os componentes que são usados para criar editores: componentes que formam as interfaces que o administrador da loja irá usar para configurar um componente.

#### src/utils/

Componentes React utilitários e outros arquivos Javascript.

## Arquivos de configuração

#### storefront/components/

Ficam todas os descritores dos componentes, meta-arquivos que indicam como um componente deve ser carregado, onde pode ser carregado e quais são as suas dependências.

#### storefront/routes/

Nessa pasta estão as configurações de rota: nome da rota e o path relacionado. Por exemplo, podemos dizer que a rota de nome "home" esta associada ao path "/".

#### storefront/settings/

Nesta pasta ficam todas as configurações **default** dos componentes da app.

* `storefront/settings/components/`: Ficam todas as configurações globais de componentes da app. Se quero que Banner@vtex.banner tenha o mesmo comportamento para toda a loja é aqui que devo configurá-lo.

* `storefront/settings/routes/`: Ficam todas as configurações dos componentes de uma página. É como dizer que para uma página específica o componente possui um set de configurações que podem não ser iguais ao de outras páginas.

## Arquivos do projeto

#### .eslintrc

Arquivo de configuração do eslint.

#### .gitignore

Arquivo importante caso use git, ferramenta de versionamento de código.

#### .vtexignore

O `.vtexignore` impede que arquivos sejam enviados para a Gallery desnecessariamente. Note que a pasta `src/` está incluida nessa lista, pois esse é o código fonte não processado: o que queremos enviar são apenas os arquivos gerados pelo Webpack, que são arquivos compilados, minificados e otimizados que vão morar dentro da pasta `storefront/assets/`.

O `.vtexignore` usa uma sintaxe idêntica ao `.gitignore` — caso queira saber mais, veja a [documentação oficial do Git](https://git-scm.com/docs/gitignore#_pattern_format).

#### package.json

Arquivo necessário para projetos Javascript que usam o npm, o package manager de Javascript.

#### webpack.config.js

Esse arquivo possui todas as configurações do Webpack.

## Buildando o código fonte

Para fazer o build do projeto vamos usar o Webpack.

Abra o terminal na pasta de seu app e rode o webpack (por padrão, ele está dando watch na pasta `src/`):
```sh
./node_modules/.bin/webpack
```

Você pode ver que quatro arquivos foram criados na pasta `storefront/assets/`. Todos eles são códigos Javascript minificados com respectivos *source maps* (arquivos que facilitam debugar o código em ferramentas como o Chrome Developer Tools). Perceba que mesmo tendo arquivos LESS no código fonte, nos arquivos gerados existem apenas arquivos Javascript. O Webpack coloca todo o código CSS dentro do Javascript para se alavancar do cache do browser. Ele também se encarrega de inserir o CSS no código HTML, fazendo com que tudo funcione normalmente.

Agora que temos os arquivos dentro da pasta `storefront/assets/`, podemos enviá-los para a Gallery.

Cancele o processo do webpack ou abra outra aba do terminal e digite:

```sh
vtex watch
```

E confira tudo funcionando no browser.

## Toolbelt ao resgate

Ganhamos a facilidade de escrever em ES6, JSX, LESS, minificar, etc, mas agora temos dois processos rodando, o watch do Toolbelt e o Webpack. Pensando em facilitar ainda mais o desenvolvimento, o Toobelt possui uma opção para quem usa Webpack.

Abra o terminal na pasta de seu app e digite:
```sh
vtex watch --webpack
```

Dessa forma, o Toolbelt se encarrega de rodar o Webpack e fazer o upload dos arquivos.

## Mais rápido! Mais rápido!

Ainda não estamos rápidos o suficiente, vamos usar um dos grandes diferenciais do combo Webpack+React, o hot-loader.

Pare o Toolbelt que está rodando e ligue-o novamente com a flag `--server` (ou `-s`):
```
vtex watch --server
```

Essa opção liga um servidor local, o Webpack Dev Server, que permite utilizar o hot-loader. Normalmente quando desenvolvemos em servidores locais acessamos URLs como `http://localhost:3000/`, no nosso caso, vamos usar a URL que Toolbelt disponibiliza para nós no terminal.

Faça uma alteração no componente `HomePage.js` ou em um arquivo CSS e veja as mudanças aplicadas sem dar reload na página.

---

### Recaptulando

Você completou o "Melhorando o processo de desenvolvimento"! Agora estamos desenvolvendo de forma eficiente e produtiva.

---
### Próximos passos

Antes de colocar a mão na massa vamos entender um pouco melhor [como o ambiente de desenvolvimento funciona](/como-funciona-o-ambiente-de-desenvolvimento.md).
