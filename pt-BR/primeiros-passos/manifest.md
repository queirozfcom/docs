# Criando um Manifest

Vamos criar nosso primeiro app no Storefront.

Cria uma pasta para o app. Nesta pasta crie um arquivo chamado `manifest.json`.

## manifest.json

Este é um arquivo fundamental de uma app VTEX. Nele é definido o nome, descrição, versão e outras informações importantes sobre o app.

Exemplo do manifest do app [vtex.storefront-theme](https://github.com/vtex-apps/theme):
```json
{
  "name": "theme",
  "vendor": "vtex",
  "version": "0.7.0",
  "title": "Default Storefront theme",
  "description": "A good place to start developing your store.",
  "dependencies": {
    "vtex.storefront": "0",
    "vtex.storefront-sdk": "0",
    "vtex.editor":"0.x",
    "vtex.banner": "0.x"
  }
}
```

### vendor

O vendor é o nome da conta que você pertence como desenvolvedor. Por exemplo, se você trabalha na VTEX, será "vtex", se você trabalha na Profite, provavelmente será "profite".

### name

Esse é o nome de seu app. Junto com o vendor, temos o nome completo de seu app, ex: "vtex.storefront-theme".

### version

É a versão de seu app. Por favor dedique um pouco de seu tempo para ler o [Semver](http://semver.org/), ele especifica como você deve versionar um projeto.

### title

Nome amigável.

### description

Descrição.

### dependencies

Aqui são listados os apps que seu app tem como dependência.

---

Crie o seu manifest.json com:

```json
{
  "name": "my-first-app",
  "vendor": "mycompany",
  "title": "My first app",
  "description": "My first app using Storefront",
  "version": "0.0.0",
  "dependencies": {
    "vtex.storefront": "0",
    "vtex.storefront-sdk": "0"
  }
}
```

Ao desenvolver um app no Storefront você **deve** colocar "vtex.storefront" e "vtex.storefront-sdk" como dependências.

**Aviso:** Durante os exemplos da documentação, lembre-se sempre de substituir o "my-first-app" e o "mycompany" com o nome que escolheu para o _name_ e _vendor_.

---

### Próximos Passos

Agora seu app está identificado e pronto para ser desenvolvido. Vamos criar o [package.json](package.md).
