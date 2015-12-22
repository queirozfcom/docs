# Area

Para que o Storefront saiba qual componente irá atender a uma determinada rota precisamos estabeler uma associação entre os dois.

Esta associação é feita através de uma configuração. As configurações ficam em uma pasta chamada `areas`.

Crie a pasta `areas` dentro da pasta `storefront`. Você terá algo assim:

```sh
├── manifest.json
└── storefront/
    ├── areas/
    ├── assets/
    │   ├── HomePage.js
    │   └── HomePage.jsx
    ├── components/
    │   └── HomePage.json
    └── routes/
        └── home.json
```

Em `areas` crie o arquivo `home.json`. O nome desse arquivo de área deve ser igual ao nome da rota que irá atender.

###`home.json`

```json
{
  "component": "HomePage@mycompany.my-first-app"
}
```

Agora você disse ao Storefront qual descritor de componente entregar quando determinada _rota_ for atendida.


## Recapitulando

Nos passos anteriores nós criamos um componente React, declaramos quais são os recursos necessários no seu carregamento e criamos uma rota. Agora estabelecemos uma associação entre o componente e a rota.

Ao abrir a página `www.loja.com/`, a rota "home" atende a esta URL. O Stoferont irá buscar o componente da área "home" (`storefront/areas/home.json`), neste caso "HomePage@vtex.my-first-app". O descritor deste componente será analisado e irá  carregar todos os seus assets (neste caso, apenas `HomePage.js`).

### Próximos passos

Estamos quase prontos para visualizar nossa primeira página. Vamos aprender a [usar o Toolbelt](toolbelt.md).
