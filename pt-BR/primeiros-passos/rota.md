# Rota

Vamos criar um arquivo de rota. Uma rota representa um caminho para encontrar uma URL.

Exemplo do arquivo de rota da página de produto:

### `product.json`

```json
{
  "path": "/:slug/p"
}
```

### path

O arquivo de rotas só possui a propriedade `path`. Nela é esperado para quais paths a rota irá atender.

Exemplo de paths e quais rotas ela atende:

Path | Atende a URL | Não atende a URL
---|---|---
_/_|www.loja.com_/_|www.loja.com/produto
_/**:slug**/p_|www.loja.com_/**havainas-preta**/p_|www.loja.com/produto
_/produto_|www.loja.com_/produto_|www.loja.com/p
_/**\*\***/c_|www.loja.com_/**camisetas/lisas**/c_|www.loja.com/contato

---

Crie o arquivo `home.json` em `storefront/routes/` com:

### `home.json`

```json
{
  "path": "/"
}
```

A rota de nome `home`, irá atender a URL `https://www.loja.com/`.

---

### Próximos passos

Criamos a rota `home`. Vamos agora atribuir qual ...
