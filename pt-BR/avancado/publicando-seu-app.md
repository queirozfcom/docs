# Publicando seu app

As instruções abaixo são úteis para quem usa nosso arquivo de configuração do **webpack**. Caso prefira usar outro _tooling_ para concatenar, minificar e/ou compilar seus arquivos não se esqueça de executá-lo antes de publicar seu app.

Para publicar um app siga os passos:

1. Mudar a versão no manifest. Consulte o [SemVer](http://semver.org/) para saber como versionar.
2. Digite o comando no terminal (usuários:
    **Linux**: `NODE_ENV=production webpack`
     **Windows**: `SET NODE_ENV=production webpack`
3. `vtex publish`