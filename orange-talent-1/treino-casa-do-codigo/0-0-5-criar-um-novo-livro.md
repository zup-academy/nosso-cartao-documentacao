### **necessidades**

*   Um título
*   Um resumo do que vai ser encontrado no livro
*   Um sumário de tamanho livre. O texto deve entrar no formato markdown, que é uma string. Dessa forma ele pode ser formatado depois da maneira apropriada.
*   Preço do livro
*   Número de páginas
*   Isbn(identificador do livro)
*   Data que ele deve entrar no ar(de publicação)
*   Um livro pertence a uma categoria
*   Um livro é de um autor

### **restrições**

*   Título é obrigatório
*   Título é único
*   Resumo é obrigatório e tem no máximo 500 caracteres
*   Sumário é de tamanho livre.
*   Preço é obrigatório e o mínimo é de 20
*   Número de páginas é obrigatória e o mínimo é de 100
*   Isbn é obrigatório, formato livre
*   Isbn é único
*   Data que vai entrar no ar precisa ser no futuro
*   A categoria não pode ser nula
*   O autor não pode ser nulo

### **resultado esperado**

*   Um novo livro precisa ser criado e status 200 retornado
*   Caso alguma restrição não seja atendida, retorne 400 e um json informando os problemas de validação

### **sobre a utilização do material de suporte aqui**

Esta é uma feature também bem parecida com o cadastro de categoria e autor. Por mais que ela tenha bem mais campos, os conhecimentos necessários para a implementação são os mesmos. Tente muito fazer sem olhar nenhum material de suporte. Se estiver complicado, tenta mais um pouco. É neste momento de busca da informação e organização das informações que já temos que o conhecimento vai se consolidando. 

Caso sinta que precisa de suporte, utilize o material de suporte de maneira bem progressiva. Lembre que também temos nosso canal do discord e você pode pedir uma ajudinha por lá :). 

**informações de suporte para a feature**

1.  [Controllers 100% coesos](https://youtu.be/i3Au8Slv3x4) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://youtu.be/_CvFy3ypsYc)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://youtu.be/2Oc56btUWQA). Neste caso aqui usar a ideia do Form Value Object é ainda mais interessante. Um livro precisa de autor, categoria etc. O código de transformação tem um esforço de entendimento ainda maior.
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://youtu.be/pu9zErRwk7k) e depois [aqui](https://youtu.be/odzqRwdgVUw)
5.  O livro tem muitas informações obrigatórias. Aqui a palavra chave é **obrigatoriedade. **Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://youtu.be/-eVRkz-3nCQ)
6.  Um construtor com muitos argumentos de tipo parecido pode gerar dificuldade para uma pessoa acertar a ordem dos parâmetros. Que tal você olhar para um pattern escrito no livro Design Patterns chamado Builder?
7.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. Um email por exemplo. Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://youtu.be/TqaMn9jTRU0)? Lembre que se tiver optado pelo construtor, a pista fica ainda mais importante dado o número de argumentos que são necessários.
8.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://youtu.be/YXF8Ll64tfk)
9.  Lembre que aqui você precisa receber uma data como argumento e, em geral, o seu framework não vai saber automaticamente qual formato ele deve se basear para pegar o texto e transformar para um objeto que represente a data em si na sua linguagem. Você deve precisar configurar.
10.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
11.  [Pegue cada uma das classes que você criou e realize a contagem da carga intrínseca](https://youtu.be/lkaK8IL7uEA). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.
12.  [Como Alberto faria esse código?](https://youtu.be/iffPcqa0WoQ)

### informações de suporte para a combinação Java/Kotlin + Spring

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  Se você tiver um atributo do tipo LocalDate,LocalDateTime etc e tiver recebendo os dados como JSON, vai precisar usar a annotation **_@JsonFormat_**(pattern = "padrao da data aqui", shape = Shape.STRING)​
5.  Se você tiver recebendo os dados da maneira tradicional, ou seja via form-url-encoded vai precisar usar a annotation **_@DateTimeFormat_**
6.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/LlX6zoGwQQA)

### sensações

Aqui, mesmo com muito mais informações, você deve ter tido de novo um pouco daquele sentimento robótico. E aí a gente se questiona, mas não é um trabalho criativo? Não o tempo todo. Não só em desenvolvimento de software, como em qualquer outro trabalho considerado criativo, os momentos onde você vai realmente precisa combinar conhecimentos de uma forma diferente para sair com uma solução da cartola são escassos. O que você precisa estar é preparado(a)! 

O código estar ficando mais fácil é um sinal que você está dominando mais as habilidades necessárias para fazer api's web, o framework, a linguagem etc. Quando aparecer uma funcionalidade mais complicada, você vai ter mais chance de performar melhor.
