# Escopo da página

As configurações que pertencem ao escopo de página são válidas somente para componentes vinculados a uma rota. Um dos benefícios é permitir que o comportamento de uma página seja totalmente diferente do restante da loja.

A resolução das configurações é simples: ganha o mais específico. Isso quer dizer que se caso a app `Shelf@vtex.shelf` declarar uma configuração e no placeholder existir uma mesma chave, a do placeholder terá precedência.

## Configurando um componente específico

O trecho abaixo configura somente o componente `Shelf@vtex.shelf` que está dentro do [placeholder](placeholders.md) `shelf` no componente `HomePage@vtex.theme`.

`storefront/settings/routes/HomePage@vtex.theme`
```sh
├── meta.json
└── storefront/
    ├── settings/
    │   └── routes/
    |       └── home/
    |           └── HomePage@vtex.theme/
    |               └── shelf.json
    └── routes/
        └── home.json
```

`storefront/settings/routes/home/HomePage@vtex.theme/shelf.json`
```json
{
   "component": "Shelf@vtex.shelf",
   "settings": {
        "title": "This is an amazing shelf!"
   }
}
```

### Configurando níveis internos

Voce também pode configurar placeholders em níveis mais internos da árvore de componentes.
Neste exemplo, o componente `Product@vtex.shelf` está dentro de um placeholder em `Shelf@vtex.shelf`. 
Com esse raciocínio seria possível alterar um componente de um placeholder dentro de `Product@vtex.shelf` e assim por diante.

`storefront/settings/routes/home/HomePage@vtex.theme`
```sh
├── meta.json
└── storefront/
    ├── settings/
    │   └── routes/
    |       └── home/
    |           └── HomePage@vtex.theme/
    |               └── shelf/
    |                   └── product.json   
    |                       └── shelf.json
    └── routes/
        └── home.json
```

`storefront/settings/routes/home/HomePage@vtex.theme/shelf/product.json`
```json
{
   "component": "Product@vtex.shelf",
   "settings": {
        "showPrice": true
   }
}
```

### Configurando componente para toda a página

Nós podemos também adicionar configurações para todos os componentes `Shelf@vtex.shelf` que aparecem na página como comportamentos _globais por página_. No exemplo abaixo estamos dizendo que para todas as shelfs os placeholders `product-list` terão a mesma configuração.

`storefront/settings/routes/home/Shelf@vtex.shelf`
```sh
├── meta.json
└── storefront/
    ├── settings/
    │   └── routes/
    |         └── home/
    |               ├── Shelf@vtex.shelf/
    |               |   └── product-list.json    
    |               └── HomePage@vtex.theme/
    |                   └── shelf/
    |                       ├── product.json   
    |                       └── shelf.json
    └── routes/
```

`storefront/settings/routes/home/Shelf@vtex.shelf/product-list.json`
```json
{
   "component": "ProductList@vtex.shelf",
   "settings": {
        "quantity": 5,
        "scroll": true,
        "arrows": {
            "right": "blue",
            "left": "red"
        }
   }
}
```
---

## Recapitulando

Nos passos anteriores conhecemos o poder dos [pontos de extensão](ponto-de-extensao.md) e aprendemos como usá-los através de [placeholders](placeholders.md).

Quando extendemos uma app também herdamos as suas configurações _default_. Desta forma, podemos sobrescrever as configurações que quisermos.

Ao sobrescrever estas configurações temos uma ordem de precedência: o mais específico sempre vence. Assim, configurações mais locais sempre irão ganhar de configurações default da app.

Com isso, temos os níveis de precedência das configurações entre apps: 

1. Configurações feitas pelo _usuário_ são mais importantes que configurações da _página_
2. Configurações da _página_ tem precendencia sobre configurações _globais de componentes_

---

## Próximos passos

Agora vamos aprender como [configurar componentes globalmente](/escopo-global.md) em uma página.

---