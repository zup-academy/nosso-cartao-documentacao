# A versão mais eficiente de um(a) dev desenvolve o que foi combinado

A prática completa é esta: **A versão mais eficiente de uma pessoa programando é aquela que entende, questiona e implementa estritamente o que foi combinado. Não inventamos coisas que não foram pedidas, não fazemos suposição de funcionalidade e nem caímos na armadilha de achar que entendemos mais do que a pessoa que solicitou a funcionalidade.**

Esse é um pilar mais comportamental do que técnico. Uma pessoa que desenvolve reune habilidades necessárias para automatizar desejos de clientes que gostariam de abandonar algum determinado fluxo manual. 

Todo software é a automação de algum processo que poderia ser feito manualmente. E aqui você pode ir para os vários de tipos de projetos.

* Uma biblioteca automatiza um determinado fluxo de código que todo(a) dev teria que fazer repetidamente;
* Um framework automatiza diversos fluxos de código que todo(a) dev teria que fazer repetidamente;
* Um software para um cliente final automatiza um fluxo manual que deve ter deve ter ficado muito complicado ou que já nasce tão complicado que precisa de automação;
* Insira qualquer outro fluxo aqui :);

## Você precisa entender exatamente o que é necessário

No livro Domain Driven Design, Eric Evans traz nos primeiros capítulos a importância de sermos ótimos "digestores" de domínio. Eu diria que precisamos também ser ótimos "digestores" de funcionalidades. Além de entender o contexto que você está inserido(a), você precisa entender o motivo de cada uma das funcionalidades que aparecerão na sua frente. 

Quando pensamos neste entendimento, existem alguns fatores que podem ser levados em consideração e que podem ficar na sua mente:

* Por que vamos fazer aquilo? [Aqui você pode tentar fazer uma análise de causa raiz](http://www.ammainc.org/wp-content/uploads/2013/02/Root_Cause.pdf) para verificar se existe realmente aquela necessidade. 

* Em geral apenas um porque tende a ser superficial. Busque pelo menos o segundo :). 

* Dado que você sabe o motivo, busque saber quais são as restrições. 
    * Tem requisito de performance?
    * Tem requisito de escalabilidade?
    * Quem pode acessar isso?
    * Preciso falar com alguém para liberar algo?
    * Quaisquer outras possíveis restrições que venham na sua cabeça.

* Qual é exatamente o resultado final esperado?

* Questione sempre que você discordar ou achar que tem algo que pode ser feito melhor em relação ao que está sendo proposto;

Como podemos automatizar um fluxo se a gente não tiver conseguido entender o desejo de automação direito? Simplesmente é um risco desnecessário. 

## Implemente o que foi combinado

Chegamos no cenário onde você entendeu exatamente o que foi pedido, dissecou a funcionalidade, questionou, debateu e, junto com as pessoas envolvidas, chegou a conclusão que precisa mesmo fazer aquilo.

Uma vez que tiver neste ponto lembre de implementar exatamente o que foi pedido. Utilize suas técnias de desenvolvimento de código para fazer um código suficiente para a funcionalidade, mantendo a dificuldade de entendimento baixa. 

Não faça mais nem menos do que foi combinado. De novo, se você, no meio da implementação, perceber qualquer coisa que você acha que poderia ser melhor ou até que está errado, vai lá e fale com as pessoas envolvidas. 

Devs eficientes não inventam fluxos, não ficam imaginam que o cliente vai mudar de ideia e nem fazem códigos baseados na esperança que aquilo um dia vai ser útil. Devs eficientes olham de maneira criteriosa para a funcionalidade, descobrem o valor daquilo para o negócio e fazem código que suporta aquele desejo. 

## Dev não é um artista?

Muito se fala que a profissão de desenvolvedor(a) é muito criativa e que pode ser comparada com pinturas, criar uma música etc. É importante que a gente se lembre que quadros e músicas também são encomendados. E quando um cliente encomenda um quadro ou uma música, a pessoa que vai produzir precisa entender exatamente o objetivo, os motivos e sair do outro lado com o resultado esperado. 

Ser comparado(a) a um(a) artista não quer dizer que fazemos o que queremos, ser comparado(a) a um(a) artista significa que temos muitas maneiras de resolver um mesmo problema e podemos usar nosso repertório para chegar lá. 



