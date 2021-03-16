### Necessidades

*   Toda categoria precisa de um nome

### Restrições

*   O nome é obrigatório
*   O nome não pode ser duplicado

### Resultado esperado

*   Uma nova categoria cadastrada no sistema e status 200 retorno
*   Caso alguma restrição não seja atendida, retorne 400 e um json informando os problemas de validação

### Sobre a utilização do material de suporte aqui

Esta é uma feature bem parecida com a de cadastro de autor. Tente implementar inicialmente sem utilizar nenhum material de suporte. Caso sinta dificuldade vá utilizando de acordo com a necessidade.

### Antes de começar

Por favor descreva como você pretende realizar a implementação deste desafio. Para acessar o formulário [clique aqui](https://forms.gle/fxHRjiS1KEHJAd5Z8)

### Informações de suporte geral

1.  [Controllers 100% coesos](https://youtu.be/NNKG2TFctfo) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://youtu.be/AzyHKZwNg1A)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://youtu.be/kzjSxBDQXp8).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://youtu.be/XPXOhvrJT1w) e depois [aqui](https://youtu.be/kkKqo80whqo)
5.  Nome é obrigatório. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://youtu.be/NoKjl0xMt6w)
6.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. O nome aqui é obrigatório, mas você não consegue garantir isso em tempo de compilação(caso esteja utilizando uma linguagem compilada). Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://youtu.be/iU19qJeXnVo)?
7.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://youtu.be/SygOC4d_N5w)
8.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
10.  [Como Alberto faria esse código?](https://youtu.be/beucXcVOcfE)

### Informações de suporte para Spring + JPA

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/H6aM-4RaRrE)

### Depois de finalizar

Antes de passar para a próxima funcionalidade, envie o link para o diff da sua solução acessando [este formulário](https://forms.gle/beXvFuHAwU3GnuMT6)

### Sensações

Talvez aqui você tenha achado que o código foi até meio repetitivo. E a verdade é que foi mesmo. Talvez no próximo você ache que foi até meio robótico, vai ser melhor ainda. Quanto mais automático você sente que é para fazer algo quer dizer que mais dominado aquilo está. O que você precisa sempre se questionar é: Será que este padrão ​ainda pode melhorar?
