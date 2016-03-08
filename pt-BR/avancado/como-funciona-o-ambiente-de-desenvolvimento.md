# Como funciona o ambiente de desenvolvimento

O ambiente de desenvolvimento do Storefront foi pensado para prover mais velocidade e praticidade aos desenvolvedores. Um desenvolvedor pode construir e ver imediatamente como as suas modificações refletem no estado final da app.

Apps adicionados ou alteradas em seu ambiente de desenvolvimento **nunca aparecerão em produção** — apenas quando forem publicadas na Gallery.

## Ativando o app no ambiente de desenvolvimento

Depois de rodar o [setup inicial](primeiros-passos/setup.md) em seu projeto, você irá usar o Toolbelt para visualizar seu app rodando no ambiente de desenvolvimento.

Criamos o cenário abaixo apenas para ilustrar o fluxo de desenvolvimento -- você pode vê-lo na prática no tutorial básico de [Primeiros Passos](../primeiros-passos).

Digamos que você queira desenvolver um app para que usuários deixem Reviews em cada produto da loja -- para tal, este app deve aparecer em todas as suas páginas de produto.

![Gráfico com app de review aparecendo na página de produto](pagina_produto_com_app.png)

Para visualizar as alterações em sua loja você irá subir o app em um **ambiente de desenvolvimento**. O seu ambiente de desenvolvimento é fácil de ser acessado e compartilhado: adicione a queryString `?workspace=sb_email@domonio.com` para indicar qual o ambiente deseja acessar.

O seu ambiente de desenvolvimento **sempre** será vinculado ao e-mail que você escreveu no `vtex login`.

## Visualizando alterações

> OK, agora o app está no ambiente de desenvolvimento de minha loja... mas como faço para que apareça de fato em minha página de produto?

![Gráfico mostrando o fluxo do toolbelt subindo o app](pagina_produto_terminal.png)

Isto depende de como o tema da sua loja (que também é um app!) foi desenvolvido:

 - Caso sua loja use um tema `Flexível` e possua um componente [Placeholder](/placeholders.md) na página de produto, basta entrar no **Modo de Edição** e configurar o placeholder para exibir o app desejada dentro dela.

 Lembre-se que o app só estará no ambiente de desenvolvimento, então outros usuários não poderão vê-la.

![Gráfico mostrando edição da página de produto e seleção do review](pagina_produto_adicionando-app.png)

 - Caso seu tema não seja `Flexível`, você precisará do seu código-fonte para editá-lo localmente. Neste caso, você deverá importar o app dentro de seu tema e rodar o Tema em uma segunda instância do Toolbelt, como exemplificado no esquema abaixo.

![Gráfico mostrando dois terminais rodando com tema e app sendo pushed](pagina_produto_app-e-tema-pelo-toolbelt.png)

Ao terminar o desenvolvimento de seu app, você pode usar o comando `vtex publish` para deixá-lo disponível a lojas pela Gallery.

---

### Recaptulando

Você completou o "Como funciona o ambiente desenvolvimento"! Agora entendemos como meus arquivos não afetam a loja em produção.

---

### Próximos passos

Vamos aprender como [criar uma nova página](/criando-uma-nova-pagina.md)