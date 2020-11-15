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

1.  [Controllers 100% coesos](https://drive.google.com/file/d/10f3lT3lB2CEXdyss7ZjeSVzmDkzEU57d/view?usp=sharing) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://drive.google.com/file/d/1SMwN_Dd9MdWI047o5dGJuBdPygbc6giX/view?usp=sharing)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://drive.google.com/file/d/18Mu6IG0CzuDtTjoPsFJWscOxG2LZvv6O/view?usp=sharing).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://drive.google.com/file/d/1P_860b6FL8mIj9X8yyQyW4B2YNL2kW5V/view?usp=sharing) e depois [aqui](https://drive.google.com/file/d/1BgjdHCbrPP8ZuTRLi5tn2a7iPepr1sCR/view?usp=sharing)
5.  Nome é obrigatório. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://drive.google.com/file/d/1988eYtK-AqS6FVET1zO04HzjM6egHoKM/view?usp=sharing)
6.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. O nome aqui é obrigatório, mas você não consegue garantir isso em tempo de compilação(caso esteja utilizando uma linguagem compilada). Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://drive.google.com/file/d/1TMENbD2V_87FmEGzwjTb4zqUnucsDnKM/view?usp=sharing)?
7.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://drive.google.com/file/d/1wc5ChsPeGFjqypb9QI7tGRMl9dn0WkkL/view?usp=sharing)
8.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
10.  [Como Alberto faria esse código?](https://drive.google.com/file/d/1TSB51AII9jqr_frkH5kgSfBu15_0d2FS/view?usp=sharing)

### informações de suporte para Spring + JPA

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://drive.google.com/file/d/18q7IUF1EmeGrPFAab1CHIXP3COf5KNHd/view?usp=sharing)

### sensações

Talvez aqui você tenha achado que o código foi até meio repetitivo. E a verdade é que foi mesmo. Talvez no próximo você ache que foi até meio robótico, vai ser melhor ainda. Quanto mais automático você sente que é para fazer algo quer dizer que mais dominado aquilo está. O que você precisa sempre se questionar é: Será que este padrão ​ainda pode melhorar?