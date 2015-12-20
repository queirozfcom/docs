# Descritor do Componente

Agora vamos criar o  primeiro arquivo de configuração, o **descritor** do componente. Este descritor é responsável por dizer ao Storefront o que o componente React precisa para ser carregado.

Dentro da pasta `storefront`, crie a pasta `components`. Você terá algo assim:

```sh
├── manifest.json
└── storefront/
    ├── assets/
    └── components/
```

Em `components` crie o arquivo `HomePage.json`. Por convenção usamos o nome do arquivo com o mesmo nome do componente React.

###`HomePage.json`

```json
{
  "assets": [
    "HomePage.js"
  ]
}
```

Em `assets` definimos quais arquivos são necessários para o carregamento do componente. Com isso, o Storefront já sabe quais arquivos precisa entregar.

## Recapitulando

No passo anterior criamos um componente React. Agora definimos quais são os arquivos necessários para seu carregamento no Storefront.

---

### Próximos Passos

Criamos nosso primeiro arquivo de configuração, o descritor do componente. Vamos agora criar a sua [rota](rota.md).
