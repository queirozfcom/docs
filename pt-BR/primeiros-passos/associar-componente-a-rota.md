# Associar componente a rota

Para que o Storefront saiba qual componente irá atender a uma determinada rota precisamos estabeler uma associação entre os dois.

Esta associação é feita através de uma configuração. As configurações ficam em uma pasta chamada areas.

Crie a pasta `areas` dentro da pasta `storefront`. Você terá algo assim:

```sh
├── manifest.json
└── storefront/
    ├── areas/
    └── assets/
    └── components/
```

Em `areas` crie o arquivo `home.json`. Por convenção usamos o nome do arquivo com o mesmo nome da rota.

###`home.json`

```json
{
  "component": "HomePage@vtex.my-first-app"
}
```

Agora você disse ao Storefront qual componente React entregar quando determinada _rota_ for atendida.


## Recapitulando

Nos passos anteriores nós criamos um componente React, declaramos quais são os recursos necessários no seu carregamento e criamos uma rota. Agora estabelecemos uma associação entre o componente e a rota.

### Próximos passos

Estamos prontos para visualizar nossa primeira página.
