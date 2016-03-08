# Exemplo: HomePage

Este é o código fonte completo do pequeno app que construímos durante o [guia de primeiros passos](README.md).

### `meta.json`

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

### `storefront/assets/HomePage.jsx`

```js
class HomePage extends React.Component {
  render() {
    return (
      <h1>Hello world!</h1>
    );
  }
}

const components = [
  {
    name: 'HomePage@vtex.my-first-app',
    constructor: HomePage
  }
];

storefront.sdk.actions.ComponentActions.register(components);
```

### `storefront/components/HomePage.json`

```json
{
  "assets": [
    "HomePage.js"
  ]
}
```

### `storefront/routes/home.json`

```json
{
  "path": "/"
}
```

### `storefront/settings/routes/home/Root@storefront-sdk/content.json`

```json
{
  "component": "HomePage@vtex.my-first-app"
}
```
