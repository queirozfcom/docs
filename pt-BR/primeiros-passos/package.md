### Package.json

Usamos o [npm](https://www.npmjs.com/) como gerenciador de pacotes. Desta forma, você pode com facilidade adicionar dependências
aos diferentes pacotes disponibilizados.

Crie  na pasta raiz o arquivo `package.json`.

Você deve ter algo assim:

```sh
├── manifest.json
└── package.json
```

Como precisamos do _React_ para renderizar o componente _HomePage_ vamos declarar como dependência no arquivo.

Exemplo de um package.json mínimo para um projeto chamado `"sample-project"`. Você pode copiá-lo e adaptá-lo para seu uso. 

```json
{
  "name": "sample-project",
  "description": "Sample project to showcase storefront functionality",
  "version": null,
  "private": true,
  "devDependencies": {
    "react": "^0.14.0"
  },
  "babel":{
    "presets": ["react","es2015"]
  }
}

```

Para instalar os pacotes basta digitar `npm i` no mesmo diretório do `package.json`.

---

### Próximos Passos

Agora seu app está identificado e pronto para ser desenvolvido. Vamos criar nosso [primeiro componente React](componente-react.md).
