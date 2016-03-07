# Toolbelt

O Toolbelt é a ferramenta que você irá utilizar durante o desenvolvimento de apps.
O Toolbelt consiste basicamente de 4 comandos:

- `vtex login` e `vtex logout`
- `vtex watch`
- `vtex publish`

### `login` e `logout`

Como o próprio nome já diz, são comandos de login e logout no ambiente de desenvolvimento.

Você pode desenvolver em apenas um loja por vez.

### `watch`

Este é o comando mais usado do Toolbelt. Ele serve para sincronizar os arquivos locais do app com o ambiente de desenvolvimento da Gallery.

Ao rodar o `vtex watch`, qualquer alteração nos arquivos faz com que eles sejam enviados para o servidor.

### `publish`

Quando seu app tiver pronto, basta usar o comando `publish` para publicá-lo na Gallery.

---

## Visualizando as alterações

Rode `vtex login` para se logar no ambiente de desenvolvimento.

```sh
$ vtex login
Please log in with your VTEX credentials:
account: dreamstore // nossa loja de teste
login: email@dominio.com  // seu email registrado na loja de teste. Email padrão geralmente usado nas outras lojas.
password - ******
```

Após fazer login, rode o comando `vtex watch` para enviar os arquivos para o ambiente de desenvolvimento.

Por fim, abra a URL que o Toolbelt mostra em seu terminal.

`http://{account}.beta.myvtex.com/?workspace=sb_email@domonio.com`

## Workspace de desenvolvimento

O queryString `?workspace=sb_email@domonio.com` da URL indica ao servidor qual o workspace deseja acessar.
O seu workspace de desenvolvimento **sempre** será vinculado ao e-mail que você escreveu no `vtex login`.

Você deve ter visto uma tela de erro. Vamos explicar e corrigir no próximo passo.

---

### Próximos Passos

Aprendemos a usar o Toolbelt. Agora vamos corrigir o erro que está na tela [registrando o componente](registro-de-componente.md).
