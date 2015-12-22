# Descritor de Componente

Agora vamos criar o  primeiro arquivo de configuração, o **descritor** do componente. Este descritor é responsável por dizer ao Storefront o que o componente React precisa para ser carregado.

Dentro da pasta `storefront`, crie a pasta `components`. Você terá algo assim:

```sh
├── manifest.json
└── storefront/
    ├── assets/
    │   ├── HomePage.js
    │   └── HomePage.jsx
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

Em `assets` definimos quais arquivos são necessários para o carregamento do componente. Com isso, o Storefront já sabe quais arquivos precisa entregar. Note que estamos referenciando o arquivo compilado. Este arquivo será inserido no browser quando este componente estiver na página.


> Por que o Storefront não pega o arquivo "HomePage.js" automaticamente?

Um componente pode precisar de outros arquivos, como arquivos CSS, fontes, imagens e outros arquivos Javascript. Além disso, um componente pode estar em um arquivo com outro nome ou até mesmo minificado e concatenado com outros componentes (ex: `bundle.min.js`). Por simplicidade e flexibilidade, você deve indicar quais arquivos o componente precisa para que ele funcione corretamente.

## Recapitulando

No passo anterior criamos um componente React. Agora definimos quais são os arquivos necessários para seu carregamento no Storefront.

---

### Próximos Passos

Criamos nosso primeiro arquivo de configuração, o descritor do componente. Vamos agora criar a sua [rota](rota.md).
