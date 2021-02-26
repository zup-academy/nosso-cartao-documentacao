# Cadastro de categorias

### Necessidades

No mercado livre você pode criar hierarquias de categorias livres. Ex: Tecnologia -> Celulares -> Smartphones -> Android,Ios etc. Perceba que o sistema precisa ser flexível o suficiente para que essas sequências sejam criadas.

*   Toda categoria tem um nome
*   A categoria pode ter uma categoria mãe

### Restrições

*   O nome da categoria é obrigatório
*   O nome da categoria precisa ser único

### Resultado esperado

*   categoria criada e status 200 retornado pelo endpoint.
*   caso exista erros de validação, o endpoint deve retornar 400 e o json dos erros.

### Antes de começar 

Por favor descreva como você pretende realizar a implementação deste desafio. Para acessar o formulário [clique aqui](https://forms.gle/cmNZnUGtrfFAGnhu7)

### Informações de suporte geral

1.  [Controllers 100% coesos](https://youtu.be/NNKG2TFctfo) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://youtu.be/AzyHKZwNg1A)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://youtu.be/kzjSxBDQXp8). Aqui você já tem uma montagem com condicional! A categoria pode ter uma mãe, mas ela pode ser raiz e não ter também. 
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://youtu.be/XPXOhvrJT1w) e depois [aqui](https://youtu.be/kkKqo80whqo)
5.  Apenas o nome da categoria é obrigatório. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://youtu.be/NoKjl0xMt6w), mas informação natural e não obrigatória não entra :). 
6.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
8.  [Como Alberto faria esse código](https://youtu.be/mm2kRewxysY)? Aqui ainda não tem a validação do nome único
9.  [Como Alberto faria esse código generalizando a validação de valores únicos?](https://youtu.be/apbdAwm6lQE)

### informações de suporte para a combinação Java/Kotlin + Spring

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/H6aM-4RaRrE)
5.  [Como externalizar as mensagens de erro no arquivo de configuração.](https://youtu.be/FO4HnZNCvoo)

### Depois de finalizar

Antes de passar para a próxima funcionalidade, envie o link para o diff da sua solução acessando [este formulário](https://forms.gle/zZBo1qpQioTUf5FK6)
