# Toolbelt

O Toolbelt é a ferramenta que você irá utilizar durante o desenvolvimento de apps. O Toolbelt consiste basicamente de 4 comandos:

- `vtex login` e `vtex logout`
- `vtex watch`
- `vtex publish`

### `login` e `logout`

Como o próprio nome já diz, são comandos de login e logout no ambiente de desenvolvimento.

Você pode desenvolver apenas um loja por vez.

### `watch`

Este é o comando mais usado do Toolbelt. Ele serve para sincronizar os arquivos locais do app com o ambiente de desenvolvimento da Gallery.

Ao rodar o `vtex watch`, qualquer alteração nos arquivos faz com que eles sejam enviados para o servidor.

### `publish`

Quando seu app tiver pronto, basta usar o comando `publish` para publicá-lo na Gallery.

---

## Visualizando as alterações

Rode `vtex login` para se logar no ambiente de desenvolvimento.

Após fazer login, rode o comando `vtex watch` para enviar os arquivos para o ambiente de desenvolvimento.

Por fim, abra a URL que o Toolbelt mostra em seu terminal.

Você deve ter visto uma tela de erro. Vamos explicar e corrigir no próximo passo.

---

### Próximos Passos

Aprendemos a usar o Toolbelt. Agora vamos corrigir o erro que está na tela [registrando o componente](registro-de-componente.md).
