# Componentização e reuso

Toda a nossa plataforma foi projetada baseada no paradigma de componentes reutilizáveis. É como se tivessemamos divido a loja em pequenos pedaços funcionais que se encaixam e comunicam entre si.

Com esta componentização os desenvolvedores podem compartilhar a resolução de um problema específico com outros desenvolvedores que vão reaproveitar esta funcionalidade no seu código.

A este pedaço de código reutilizado nós demos o nome de [Apps](ecossistema.md). Uma App é um conjunto de componentes React e configurações que são construídas em pequenos blocos para resolverem um problema específico.

Apps focadas em problemas específicos possibilitam que desenvolvedores reutilizem aplicacões de terceiros e não precisem reinvetar a roda. Mas caso você não queira usar código de terceiros, o modelo de apps contribui para que os times trabalhem de forma mais eficiente, através do compartilhamento de funcionalidades por todos os projetos. 

# Pontos de extensão

Os **pontos de extensão** são contratos criados entre apps que possibilitam o encaixe de um bloco no outro.

No final, quando o usuário substiuir uma prateleira por outra, mudar a ordem dos elementos de uma app ou trocar todo o layout da página ele terá feito isso através dos pontos de extensão que você estabeleceu.

Em seguida veremos na prática como criar um ponto de extensão usando [placeholders](placeholders.md) para deixar nossas apps mais extensíveis ou adicionar uma nova funcionalidade a um app já existente.