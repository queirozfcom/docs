# Toolbelt

O Toolbelt é a ferramenta que você irá utilizar durante o desenvolvimento de apps.
O Toolbelt consiste basicamente de 4 comandos:

- `vtex login` e `vtex logout`
- `vtex watch`
- `vtex publish`

### `login` e `logout`

Como o próprio nome já diz, são comandos de login e logout no ambiente de desenvolvimento.

O `login` é um comando por sessão de desenvolvimento, portanto, é preciso logar uma única vez  para sincronizar quantas apps desejar. Lembrando que você pode desenvolver em apenas uma loja por vez, caso precise desenvolver em outra loja será necessário abandonar a sessão com o `logout`.

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

Após fazer login, rode o comando `vtex watch` (de dentro da pasta onde seu app está) para enviar os arquivos para o ambiente de desenvolvimento.

Abra a URL que o Toolbelt mostra em seu terminal.

`http://{account}.beta.myvtex.com/?workspace=sb_email@dominio.com`

Você deverá ter visto **uma tela de erro**. Vamos explicar e corrigir no próximo passo.

## Workspace de desenvolvimento

O queryString `?workspace=sb_email@dominio.com` da URL indica ao servidor qual o workspace deseja acessar.
O workspace funciona como um ambiente isolado de desenvolvimento da loja, ele **sempre** será vinculado ao e-mail que você escreveu no `vtex login`.

Desta forma, uma equipe pode trabalhar ao mesmo tempo no mesmo projeto sem que os colaboradores interfiram no trabalho um do outro.


---

### Próximos Passos

Aprendemos a usar o Toolbelt. Agora vamos corrigir o erro que está na tela [registrando o componente](registro-de-componente.md).