# Escopo de configuração

Todo componente pode ter configurações que mudam o seu comportamento. Estas configurações podem ser definidas pelo desenvolvedor durante a criação da app.

Uma boa prática é construir apps com configurações iniciais que determinam um comportamento padrão da aplicação até que o usuário possa alterá-las através de um editor.

Apps podem se alavancar de outras apps para criar funcionalidades, portanto, é natural que as configurações de uma app sejam sobrescritas pela app que a consome. 

Mas às vezes você pode querer modificar somente um valor e usar todas as configurações restantes,
em outros casos irá querer que uma app tenha o mesmo comportamento em todas as páginas. 

O escopo de configuração serve para definir o alcance das configurações (`somente na página` ou `todas as páginas`) de uma app e como ocorre a sobreposição das configurações entre apps.

O que nos deixa animados sobre *escopo de configuração* é que você pode alterar o comportamento de uma parte muito específica da app sem afetar o restante.
Por exemplo, em uma página de produto com diversas apps é possível sobrescrever ou alterar as configurações somente do app de "Preço do Produto" sem interferir nos componentes restantes.

Pode também dizer que a configuração de um componente só vale em uma página ou alterar seu comportamento para ser o mesmo em toda a loja.

As configurações de um app sempre ficam na pasta `storefront/settings` e estão dividas por _configurações de rotas_ e _configurações de componentes_.

## Configurações default

Define um estado inicial que pode ser alterado pelo usuário através de um editor.

## Configuração default de rota

Serve para configurar componentes de uma rota específica. 

## Configuração default de componentes

Serve para configurar componentes para todas rotas da app.