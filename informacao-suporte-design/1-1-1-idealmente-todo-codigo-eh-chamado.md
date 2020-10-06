# Idealmente, todo código escrito deveria ser chamado por alguém. 

A prática completa é escrita da seguinte forma: **Idealmente, todo código escrito deveria ser chamado por alguém. Se não tem ninguém chamando, ele não deveria existir.**

A ideia aqui é simples, não deveria existir classes, métodos, atributos, parâmetros e variáveis que não estão sendo utilizados. Tudo que você cria aumenta a dificulda de entendimento, então cada uma dessas coisas deveria merecer existir no sistema. 

## Evite geração de código desenfreada

Tanto pelas IDE's, quanto por bibliotecas, temos possibilidades muito interessantes de geração de código. E que fique claro: Você deve utilizar. O que você deveria evitar é simplesmente gerar porque deus quis e não refletir sobre aquilo. 

Para mitigar código que não é utilizado por ninguém, você pode abraçar de vez [a ideia de começar todo fluxo de código pelo ponto de entrada do dado](https://github.com/claudiooliveirazup/documentacao-cartao-branco/blob/master/informacao-suporte-design/0-0-3-execute-codigo-mais-rapido-possivel.md). Fazendo isso, você maximiza a chance de só escrever o que foi necessário naquele fluxo. 

## E quando fluxos forem modificados?

Funcionalidades são criadas e extintas, então é normal acabarmos com código morto dentro do nosso sitema. É uma coisa certa, justamente pela natureza de mudança contínua do software. 

A sugestão aqui é adotar como prática de desenvolvimento apagar código morto. Passou por algum lugar e percebeu que tal código não está invocado, apaga e segue a vida.
