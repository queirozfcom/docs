# Storefront Docs

O Storefront é o novo framework de desenvolvimento de sites da VTEX. Além disto, ele também traz o Storefront CMS um novo editor que permite aos usuários da plataforma editarem e configurarem seu site de maneira rápida e simplificada.

O Storefront e o Storefront CMS ainda estão em fase de testes, mas substituirão o atual Portal da VTEX.

Antes de apresentar o Storefront porém, precisamos apresentar dois conceitos fundamentais na nova plataforma da VTEX: Apps e Gallery.

### Apps

O desenvolvimento de lojas no sistema VTEX agora é totalmente baseado em Apps. 

O que é uma App? Uma app é uma aplicação ou sistema que desempenha uma funcionalidade quando instalada na loja VTEX. O layout de uma loja é nada mais é que uma App de Tema instalada em sua conta.

Apps trazem autonomia para lojistas, ao permitir que adicionem novas funcionalidades e customizem o design da loja sem depender diretamente do desenvolvimento de agências: a instalação de apps é completamente plug & play.

As apps podem trazer diversas funcionalidades para o site da loja: uma app de reviews que permite a um cliente avaliar produtos e ler avaliações de terceiros ou até mesmo uma app de tema para mudar todo o layout de sua loja em um clique.

### Gallery

A VTEX Gallery permite que desenvolvedoras e agências publiquem apps — gratuitos ou pagos — que podem ser facilmente encontrados e instalados por lojistas da VTEX.

Apps disponibilizados na Gallery são mais poderosos que as antigas extensões da VTEX Store, pois oferecem funcionalidades que podem interagir com todos os sistemas da VTEX.

### Storefront Framework

A base de desenvolvimento de apps é o StoreFront Framework, que permite a desenvolvedores e agências criar componentes editáveis que interagem de maneira fluida com todas as apps instaladas na loja e ainda podem ser configuradas pelo usuário.

O Storefront Framework pode ser pensado em duas ferramentas principais:

#### Componentes React

Todas as apps feitas para o Storefront Framework usam componentes baseados no framework React.js — com uma implementação própria do DOM e uma estrutura de aplicação otimizada, o React consegue renderizar sites com altíssima performance.

O framework React é fundamentado no conceito de componente. No contexto do StoreFront, um componente é um pedaço específico da funcionalidade de uma App.

Ao usar o React, todos os módulos de funcionalidade e interface são separados em componentes que conversam com o back-end da VTEX para renderizar uma loja (ou qualquer outra app).

Leia mais sobre o React em nosso React: Getting Started ou baixe nosso tema de exemplo, o DreamTheme para ver de perto um app desenvolvido em React.

#### Deploy contínuo com o Toolbelt

Toolbelt é uma CLI de deploy contínuo que oferece funcionalidade de live-preview durante o desenvolvimento do seu site, bem como a habilidade de publicar uma app na Gallery direto da linha de comando.

### Storefront CMS

Junto de cada App (ou Tema) desenvolvida com o Storefront Framework, o desenvolvedor deve criar um componente específico para servir como admin de configuração do App.

Isto por que, com o Storefront CMS, o usuário lojista pode acessar seu site em modo de edição e configurar seu componente — seja a imagem de um banner, a quantidade de produtos em uma prateleira ou alguma opção de layout do tema.

Como o Storefront possui uma natureza modular, o modo de edição de duas lojas podem ser completamente diferentes, dependendo dos apps e componentes instalados por cada uma.




