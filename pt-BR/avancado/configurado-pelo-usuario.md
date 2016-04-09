# Configurado pelo usuário

Quando um desenvolvedor constrói uma nova aplicação ele cria [editores](/avancados/editor.md) para que o usuário possa customizar como desejar.

Como boa prática sempre que desenvolvemos um novo app é importante que tenha **configurações iniciais** com o papel de determinar um comportamento padrão até que o usuário possa alterá-las através de um editor.

Imagine o cenário em que o usuário instale um novo app mas nada acontece porque ele precisa configurar tudo do zero. Não parece muito intuitivo, não acha? Por isso que permitimos aos desenvolvedores adicionarem configurações _default_ às suas aplicações.

## Escopo do usuário

No Storefront quando entregamos as configurações de um componente **sempre** priorizamos as realizadas pelo usuário. Neste caso, se uma configuração _default_ tiver sido sobrescrita por um editor ela será entregue com o valor que o usuário escolheu.

Por outro lado, o usuário não precisa sobrescrever todas as configurações para que um app funcione.
É por isso que entregamos a união entre o que foi alterado pelo usuário e as configurações iniciais da app.

---

## Recapitulando

Neste passo descobrimos que apps podem ter **configurações iniciais**. Estas configurações são válidas até que o usuário as tenha alterado.

O primeiro nível de precedência das configurações entre apps: 

1. Configurações feitas pelo _usuário_ são mais importantes que configurações _default da página_

---

## Próximos passos

Nos passos seguintes vamos aprender como criar as [configurações iniciais em uma página](escopo-da-pagina.md).