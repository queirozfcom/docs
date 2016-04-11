# Componentização e reuso

Toda a nossa plataforma foi projetada baseada no paradigma de componentes reutilizáveis. É como se tivessemos divido a loja em pequenos pedaços funcionais que se encaixam e comunicam entre si.

Com esta componentização os desenvolvedores podem compartilhar a resolução de um problema específico com outros desenvolvedores que vão reaproveitar esta funcionalidade no seu código.

A este pedaço de código reutilizado nós demos o nome de [Apps](ecossistema.md). Um App é um conjunto de componentes React e configurações que são construídos em pequenos blocos para resolverem um problema específico.

Apps focados em problemas específicos possibilitam que desenvolvedores reutilizem aplicacões de terceiros sem precisar reinvetar a roda.

# Pontos de extensão

Os **pontos de extensão** são contratos criados entre apps que possibilitam o encaixe de um bloco no outro.

No final, quando o usuário substiuir uma prateleira por outra, mudar a ordem dos elementos de uma app ou trocar todo o layout da página ele terá feito isso através dos pontos de extensão que você estabeleceu.

## Próximos passos

Em seguida veremos na prática como deixar nossos apps mais extensíveis usando [placeholders](placeholders.md).