# Exemplo: HomePage

Este é o código fonte completo do pequeno app que construímos durante o [guia de primeiros passos](README.md).

### `manifest.json`

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

### `package.json`

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

### `storefront/assets/HomePage.jsx`

```js
class HomePage extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello world!</h1>
      </div>
    );
  }
}

const components = [
  {
    name: 'HomePage@mycompany.my-first-app',
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

### `storefront/settings/routes/home/Root@vtex.storefront-sdk/content.json`

```json
{
  "component": "HomePage@mycompany.my-first-app"
}
```
