# Solução de problemas

# Mac e Linux

Em alguns casos, em especial no Mac e no Linux, pode ser que seja necessário usar `sudo` para instalar os pacotes node. Em geral, a falta do `sudo` é a principal razão de erros do tipo `EACCES, permission denied`.  Então, antes de todo comando que começa com `npm install -g`, use `sudo npm install -g`.


# Windows

Em alguns casos no Windows, pode dar o erro `ECONNRESET`, para solucionar digite no terminal:
```
npm config set registry http://registry.npmjs.org/
```

Agora tente instalar os pacotes novamente.
