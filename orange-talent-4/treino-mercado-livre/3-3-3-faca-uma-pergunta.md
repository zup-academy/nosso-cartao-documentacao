### **Explicação**

Um usuário logado pode fazer uma pergunta sobre o produto

### Necessidades

*   A pergunta tem um título
*   Tem instante de criação
*   O usuário que fez a pergunta
*   O produto relacionado a pergunta
*   O vendedor recebe um email com a pergunta nova
*   o email não precisa ser de verdade. Pode ser apenas um print no console do servidor com o corpo.

### Restrições

*   O título é obrigatório
*   O produto é obrigatório
*   O usuário é obrigatório

### Resultado esperado

*   Uma nova pergunta é criada e é retornada. Status 200
*   Em caso de erro de validação, retorne 400 e o json com erros.

### Antes de começar

Por favor descreva como você pretende realizar a implementação deste desafio. Para acessar o formulário [clique aqui](https://forms.gle/fd5KpTFcxALVJuW68)

### Informações de suporte geral

1.  [Controllers 100% coesos](https://youtu.be/NNKG2TFctfo) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos. Lembre que isso não quer dizer que o controller tem um método só, apenas que idealmente todos os métodos devem usar todos os atributos ou pelo menos a grande maioria deles.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://youtu.be/AzyHKZwNg1A)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://youtu.be/kzjSxBDQXp8).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://youtu.be/XPXOhvrJT1w) e depois [aqui](https://youtu.be/kkKqo80whqo)
5.  [Lembre que toda informação natural e obrigatória entra pelo construtor](https://youtu.be/NoKjl0xMt6w). Um opinião é de um usuário para um produto. Além das outras informações obrigatórias. 
6.  Na hora de enviar o email, você precisa construir as informações a partir da pergunta. Pode ser natural querer colocar esse código dentro da classe **_Pergunta _**​​e faz até muito sentido. [Deixei uma opinião aqui sobre isso](https://youtu.be/iyM12hm0Jig).
7.  Será que você pensou em listeners para resolver o envio do email? Eu sugiro que regras de negócio devem ser declaradas de maneira explícita na nossa aplicação. 
8.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
10.  Caso você já esteja utilizando um projeto de segurança. O framework da sua escolha, integrado com algum outro projeto de segurança, deve permitir que você tenha acesso ao objeto que representa o usuário logado dentro do método do seu controller. 
11.  [Como Alberto faria esse código](https://youtu.be/-twyU9WPq8w) e como [Alberto faria para enviar o email.](https://youtu.be/5xOEBFlEHik) 

### Informações de suporte para a combinação Java/Kotlin + Spring​

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/H6aM-4RaRrE)
5.  [Como externalizar as mensagens de erro no arquivo de configuração.](https://youtu.be/FO4HnZNCvoo)
6.  Use e abuse das annotations da bean validation para indicar as restrições dos parâmetros. 
7.  Brinque um pouco com a classe **_Assert_**​ ​do Spring para fazer checagens de parâmetro também. As ideias de Design By Contract ajudam demais a aumentar a confiabilidade da aplicação.
8.  Para configurar o Spring Security olhe [aqui](https://youtu.be/0I--CLsqC7w)
9.  Lembrando que, para receber a referência para o usuário logado no método do controller, você pode usar a annotation _@AuthenticationPrincipal_​.
10.  Para retornar status diferentes, consulte este material [aqui](https://youtu.be/CWe1yokaPf4)
11.  Uma solução muito utilizada no mercado para este tipo de situação é a criação de listeners. [Eu até já escrevi sobre isso muito atrás](https://domineospring.wordpress.com/2015/06/08/lidando-com-eventos-dentro-do-spring/) . Eu sempre recomendo que regras que fazem parte do fluxo de negócio fiquem explícitas, para que sejam mais facilmente encontradas.

### Depois de finalizar

Antes de passar para a próxima funcionalidade, envie o link para o diff da sua solução acessando [este formulário](https://forms.gle/HdPxdRk5XFTZXEie9)
