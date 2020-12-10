### necessidades

*   Toda categoria precisa de um nome

### restrições

*   O nome é obrigatório
*   O nome não pode ser duplicado

### resultado esperado

*   Uma nova categoria cadastrada no sistema e status 200 retorno
*   Caso alguma restrição não seja atendida, retorne 400 e um json informando os problemas de validação

### sobre a utilização do material de suporte aqui

Esta é uma feature bem parecida com a de cadastro de autor. Tente implementar inicialmente sem utilizar nenhum material de suporte. Caso sinta dificuldade vá utilizando de acordo com a necessidade. ​

### informações de suporte geral

1.  [Controllers 100% coesos](https://youtu.be/i3Au8Slv3x4) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://youtu.be/_CvFy3ypsYc)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://youtu.be/2Oc56btUWQA).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://youtu.be/pu9zErRwk7k) e depois [aqui](https://youtu.be/odzqRwdgVUw)
5.  Nome é obrigatório. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://youtu.be/-eVRkz-3nCQ)
6.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. O nome aqui é obrigatório, mas você não consegue garantir isso em tempo de compilação(caso esteja utilizando uma linguagem compilada). Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://youtu.be/TqaMn9jTRU0)?
7.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://youtu.be/YXF8Ll64tfk)
8.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
10.  [Como Alberto faria esse código?](https://youtu.be/f8IOu-jloz0)

### informações de suporte para Spring + JPA

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/LlX6zoGwQQA)

### sensações

Talvez aqui você tenha achado que o código foi até meio repetitivo. E a verdade é que foi mesmo. Talvez no próximo você ache que foi até meio robótico, vai ser melhor ainda. Quanto mais automático você sente que é para fazer algo quer dizer que mais dominado aquilo está. O que você precisa sempre se questionar é: Será que este padrão ​ainda pode melhorar?
