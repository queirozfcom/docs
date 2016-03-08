# Escopo global

O escopo global determina as configurações _default_ para todos os componentes em todas as páginas.

### Configurando componente globalmente

Para configurar um componente utilizando o escopo global é preciso criar arquivos na pasta `storefront/settings/components`.

No trecho abaixo, configuramos três placeholders com configuração _default_: header, body e footer.
Isso significa que todos os componentes `DefaultTemplate@vtex.theme` nesta app possuem as mesmas configurações para os placeholders header, body e footer.

`storefront/settings/DefaultTemplate@vtex.theme/`
```sh
    ├── meta.json
    └── storefront/
        └── settings/
            └── components/
                └── DefaultTemplate@vtex.theme/
                    ├── header.json
                    ├── body.json
                    └── footer.json
```

`storefront/settings/components/DefaultTemplate@vtex.theme/header.json`
```json
{
  "component": "Header@vtex.header",
  "settings": {
    "background": "blue",
    "categories": ["winter", "summer", "fall"]
  }
}
```

`storefront/settings/components/DefaultTemplate@vtex.theme/body.json`
```json
{
  "component": "Home@acme.theme"
}
```

`storefront/settings/components/DefaultTemplate@vtex.theme/footer.json`
```json
{
  "component": "Footer@vtex.footer"
}
```

### Sobrescrevendo as configurações de um componente global

É possível na rota sobrescrever as configurações de um componente global na app.
No exemplo estamos dizendo que o placeholder `body` na rota "home" é ocupado pelo
componente "HomePage@vtex.theme", também poderíamos dizer que na rota "product" o
placeholder `body` recebe o "ProductPage@vtex.theme".

Note que modificamos **somente** o placeholder (`body`) os outros continuam sendo
reutilizados por todas as páginas (`header` e `footer`).

`storefront/settings/home/DefaultTemplate@vtex.theme/`
```sh
├── meta.json
└── storefront/
    ├── settings/
    |   ├── components/
    |   |     └── DefaultTemplate@vtex.theme/
    |   |         ├── header.json
    |   |         ├── body.json
    |   |         └── footer.json
    │   └── routes/
    |       └── home/
    |       |   ├── DefaultTemplate@vtex.theme/
    |       |   |   └── body.json
    |       |   └── HomePage@vtex.theme/
    |       └── product/
    |           ├── DefaultTemplate@vtex.theme/
    |           |   └── body.json
    |           └── ProductPage@vtex.theme/
    |
    └── routes/
```

`storefront/settings/home/DefaultTemplate@vtex.theme/body.json`
```json
{
    "component": "HomePage@vtex.theme"
}
```

No final, os componentes `HomePage@vtex.theme` e `ProductPage@vtex.theme` terão o `header` e o 
`footer` do `DefaultTemplate@vtex.theme`.

---

## Recapitulando

Nos passos anteriores descobrimos os níveis de precedência das configurações entre apps: 

1. Configurações feitas pelo _usuário_ são mais importantes que configurações da _página_
2. Configurações _da página_ tem precendencia sobre configurações _globais de componentes_
3. Configurações da _página_ ganham quando comparadas com _globais da app_

Agora aprendemos como declarar configurações de um componente globalmente e reutilizá-las nas páginas. O escopo global é uma poderosa ferramenta para evitar o retrabalho e centralizar responsabilidades.

---