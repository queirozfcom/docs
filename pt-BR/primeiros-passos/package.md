### Package.json

Usamos o [npm](https://www.npmjs.com/) como gerenciador de pacotes. Desta forma, voce pode com facilidade adicionar dependências
aos diferentes pacotes disponibilizados.

Crie  na pasta raiz o arquivo `package.json`.

Você deve ter algo assim:

```sh
├── meta.json
└── package.json
```

Como precisamos do _React_ para renderizar o componente _HomePage_ vamos declarar como dependencia no arquivo.

Exemplo do package.json do app [vtex.storefront-theme](https://github.com/vtex-apps/theme):
```json
{
  "name": "theme",
  "description": "Default theme for new VTEX stores",
  "version": null,
  "private": true,
  "devDependencies": {
    "react": "^0.14.0"
  },
  "babel":{
    "presets": ["react"]
  }
}

```

Para instalar os pacotes basta digitar `npm i` no mesmo diretório do `package.json`.

---

### Próximos Passos

Agora seu app está identificado e pronto para ser desenvolvido. Vamos criar nosso [primeiro componente React](componente-react.md).
