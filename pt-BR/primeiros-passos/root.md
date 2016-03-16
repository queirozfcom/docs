# Componente Root

Para que o Storefront saiba qual componente irá atender a uma determinada rota precisamos estabelecer uma associação entre os dois: _rota_ e _componente_.

Esta associação é feita quando configuramos o componente nativo da plataforma: o `Root@vtex.storefront-sdk`.

O componente Root é o ponto de entrada para o carregamento de componentes de qualquer rota. Portanto, toda rota precisa ter um Root configurado.

Crie a pasta `settings/routes/` dentro da pasta `storefront`. Você terá algo assim:

```sh
├── meta.json
└── storefront/
    ├── assets/
    │   ├── HomePage.js
    │   └── HomePage.jsx
    ├── components/
    │   └── HomePage.json
    ├── settings/
    │   └── routes/
    └── routes/
        └── home.json
```

Em `storefront/routes` crie a pasta `home/Root@vtex.storefront-sdk` com o arquivo `content.json`.

```sh
├── meta.json
└── storefront/
    ├── assets/
    │   ├── HomePage.js
    │   └── HomePage.jsx
    ├── components/
    │   └── HomePage.json
    ├── settings/
    │   └── routes/
    |       └── home/
    |           └── Root@vtex.storefront-sdk/
    |               └── content.json
    └── routes/
        └── home.json
```

E no `content.json` declare:
```json
{
  "component": "HomePage@mycompany.my-first-app"
}
```

Agora você disse ao Storefront qual o componente entregar quando a _rota_ `home` for atendida.

## Recapitulando

Nos passos anteriores nós criamos um componente React, declaramos quais são os recursos necessários no seu carregamento e criamos uma rota.
Agora estabelecemos uma associação entre o componente e a rota.

Ao abrir a página `www.loja.com/`, a rota "home" atende a esta URL. O Storefront **sempre** irá buscar o componente `Root@vtex.storefront-sdk` nas configurações da rota correspondente: "home" (`storefront/settings/routes/home/Root@vtex.storefront-sdk`).

O `content` do Root expressa qual componente deve ser carregado para a rota: "HomePage@mycompany.my-first-app".

### Próximos passos

Estamos quase prontos para visualizar nossa primeira página. Vamos aprender a [usar o Toolbelt](toolbelt.md).
