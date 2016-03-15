# Rota

Queremos que nosso site atenda a URL `/`, chamaremos essa página de "home". Para isso, precisamos criar um arquivo de rota. Uma rota representa um caminho para encontrar uma URL.

Crie a pasta `routes` dentro de `storefront`. Você terá algo assim:

```sh
├── manifest.json
└── storefront/
    ├── assets/
    │   ├── HomePage.js
    │   └── HomePage.jsx
    ├── components/
    │   └── HomePage.json
    └── routes/
```

Crie o arquivo `home.json` dentro desta pasta. Diferente dos componentes, a convenção para os nomes de arquivos de rotas é [kebab-case](http://c2.com/cgi/wiki?KebabCase).

### `home.json`

```json
{
  "path": "/"
}
```

### path

O arquivo de rotas só possui a propriedade `path`. Nela é esperado para qual path a rota irá atender.

Exemplo de paths e quais rotas ela atende:

Path | Atende a URL | Não atende a URL
---|---|---
_/_|www.loja.com_/_|www.loja.com/produto
_/**:slug**/p_|www.loja.com_/**havainas-preta**/p_|www.loja.com/produto
_/produto_|www.loja.com_/produto_|www.loja.com/p
_/**\*\***/c_|www.loja.com_/**camisetas/lisas**/c_|www.loja.com/contato

---

## Recapitulando

Quando queremos que o app responda por uma rota, devemos criar um arquivo de rota dentro da pasta `storefront/routes/`. O nome da rota é o nome do arquivo.

No exemplo foi criado o arquivo `home.json` com a propriedade `path` sendo `/`. Por conta disso, quando o usuário acessar a URL `https://www.loja.com/` a página "home" será carregada.

---

### Próximos passos

Criamos a rota `home`. Vamos agora associar um componente React a uma rota [configurando o componente Root](root.md).
