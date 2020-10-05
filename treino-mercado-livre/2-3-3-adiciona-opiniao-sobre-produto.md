# Adicione uma opinião sobre um produto

### Explicação

Um usuário logado pode opinar sobre um produto. Claro que o melhor era que isso só pudesse ser feito depois da compra, mas podemos lidar com isso depois.

### Necessidades

*   Tem uma nota que vai de 1 a 5
*   Tem um título. Ex: espetacular, horrível...
*   Tem uma descrição
*   O usuário logado que fez a pergunta (aqui pode usar usar o approach de definir um usuário na primeira linha do controller e depois trabalhar com o logado de verdade)
*   O produto que para o qual a pergunta foi direcionada

### Restrições

*   A restrição óbvia é que a nota é no mínimo 1 e no máximo 5
*   Título é obrigatório
*   Descrição é obrigatório e tem no máximo 500 caracteres
*   usuário é obrigatório
*   o produto relacionado é obrigatório

### Resultado esperado

*   Uma nova opinião é criada e status 200 é retornado
*   Em caso de erro de validação, retorne 400 e o json com erros.

### **informações de suporte geral**

1.  [Controllers 100% coesos](https://drive.google.com/file/d/10f3lT3lB2CEXdyss7ZjeSVzmDkzEU57d/view?usp=sharing) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos. Lembre que isso não quer dizer que o controller tem um método só, apenas que idealmente todos os métodos devem usar todos os atributos ou pelo menos a grande maioria deles.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://drive.google.com/file/d/1SMwN_Dd9MdWI047o5dGJuBdPygbc6giX/view?usp=sharing)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://drive.google.com/file/d/18Mu6IG0CzuDtTjoPsFJWscOxG2LZvv6O/view?usp=sharing).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://drive.google.com/file/d/1P_860b6FL8mIj9X8yyQyW4B2YNL2kW5V/view?usp=sharing) e depois [aqui](https://drive.google.com/file/d/1BgjdHCbrPP8ZuTRLi5tn2a7iPepr1sCR/view?usp=sharing)
5.  [Lembre que toda informação natural e obrigatória entra pelo construtor](https://drive.google.com/file/d/1988eYtK-AqS6FVET1zO04HzjM6egHoKM/view?usp=sharing). Um opinião é de um usuário para um produto. Além das outras informações obrigatórias. 
6.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
7.  [Pegue cada uma das classes que você criou e realize a contagem da carga intrínseca](https://drive.google.com/file/d/1MwuEjVO9evwVsYK5t5hB0q22uHj7CwSQ/view?usp=sharing). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.
8.  Caso você já esteja utilizando um projeto de segurança. O framework da sua escolha, integrado com algum outro projeto de segurança, deve permitir que você tenha acesso ao objeto que representa o usuário logado dentro do método do seu controller. 
9.  [Como Alberto faria esse código](https://drive.google.com/file/d/1OWV90fkVaaI3Ip8_yQeuYz0MA36Y68XZ/view?usp=sharing)

### informações de suporte para a combinação Java/Kotlin + Spring​

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://drive.google.com/file/d/18q7IUF1EmeGrPFAab1CHIXP3COf5KNHd/view?usp=sharing)
5.  [Como externalizar as mensagens de erro no arquivo de configuração.](mailto:Como%20criar%20um%20@RestControllerAdvice%20para%20customizar%20o%20json%20de%20sa%C3%ADda%20com%20erros%20de%20valida%C3%A7%C3%A3o)
6.  Use e abuse das annotations da bean validation para indicar as restrições dos parâmetros. 
7.  Brinque um pouco com a classe **_Assert_**​ ​do Spring para fazer checagens de parâmetro também. As ideias de Design By Contract ajudam demais a aumentar a confiabilidade da aplicação.
8.  Para configurar o Spring Security olhe [aqui](https://drive.google.com/file/d/1314vY4OpQqTPAnb5fPaMCaWEYdZqpP78/view?usp=sharing)
9.  Lembrando que, para receber a referência para o usuário logado no método do controller, você pode usar a annotation _@AuthenticationPrincipal_​.
10.  Para retornar status diferentes, consulte este material [aqui](https://drive.google.com/file/d/16_FGNxrqh3ACLJtSuf7FDaSmekhpoWxE/view?usp=sharing)