# Ambiente de Desenvolvimento

O ambiente de desenvolvimento do Storefront foi pensado para garantir mais velocidade e praticidade para desenvolvedores, garantindo que seus apps possam ser facilmente validadas antes de ir para produção.

Apps adicionados ou alteradas em seu ambiente de desenvolvimento **nunca aparecerão em produção** — apenas quando forem publicadas na Gallery.

Depois de rodar o [setup inicial](primeiros-passos/setup.md) em seu projeto, você irá usar o Toolbelt para visualizar seu app rodando sobre um ambiente de testes durante o desenvolvimento.

Criamos o cenário abaixo apenas para ilustrar o fluxo de desenvolvimento -- você pode vê-lo na prática no tutorial básico de [Primeiros Passos](../primeiros-passos).

---

Digamos que você queira desenvolver um app para que usuários deixem Reviews em cada produto da loja -- para tal, este app deve aparecer em todas as suas páginas de produto.

![Gráfico com app de review aparecendo na página de produto](pagina_produto_com_app.png)


Para visualizar o app em sua loja durante o desenvolvimento, você irá subi-la em um **ambiente de desenvolvimento**, que permite que apenas seu usuário possa visualizar as alterações em desenvolvimento.

Para isso, é preciso fazer login com suas credenciais no Toolbelt e rodá-lo com o comando `watch`. seu app já estará instalada na sua loja, exclusivamente em seu ambiente de desenvolvimento. Saiba mais sobre o Toolbelt em sua [documentação oficial](https://github.com/vtex/toolbelt).

> OK, agora o app está no ambiente de desenvolvimento de minha loja... mas como faço para que apareça de fato em minha página de produto?

![Gráfico mostrando o fluxo do toolbelt subindo o app](pagina_produto_terminal.png)

Isto depende de como o tema da sua loja (que também é um app!) foi desenvolvido:

 - Caso sua loja use um tema `Flexível` e possua um componente **Área** na página de produto, basta entrar no **Modo de Edição** e configurar sua Área para exibir o app desejada dentro dela.

 Lembre-se que o app só estará no ambiente de desenvolvimento, então outros usuários não poderão vê-la.

![Gráfico mostrando edição da página de produto e seleção do review](pagina_produto_adicionando-app.png)

 - Caso seu tema não seja `Flexível`, você precisará do seu código-fonte para editá-lo localmente. Neste caso, você deverá importar o app dentro de seu tema e rodar o Tema em uma segunda instância do Toolbelt, como exemplificado no esquema abaixo.

![Gráfico mostrando dois terminais rodando com tema e app sendo pushed](pagina_produto_app-e-tema-pelo-toolbelt.png)

---

Ao terminar o desenvolvimento de seu app, você pode usar o comando `vtex publish` para deixá-lo disponível a lojas pela Gallery.
