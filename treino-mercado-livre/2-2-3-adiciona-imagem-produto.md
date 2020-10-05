# Usuário logado adiciona imagem no seu produto

### Explicação

Com um produto cadastrado, um usuário logado pode adicionar imagens ao seu produto. Não precisa salvar a imagem em algum cloud ou no próprio sistema de arquivos. Cada arquivo de imagem pode virar um link ficticio que pode ser adicionado ao produto. 

### **necessidades**

*  Adicionar uma ou mais imagens a um determinado produto do próprio usuário

### **restrições**

*  Tem uma ou mais fotos
*  Só pode adicionar fotos ao produto que pertence ao próprio usuário

### Resultado esperado

*   Imagens adicionadas e 200 como retorno
*   Caso dê erro de validação retorne 400 e o json dos erros
*   Caso tente adicionar imagens a um produto que não é seu retorne 403.

### desafio extra

Como você faria para que em dev a imagem virasse um link fictício e em produção executasse um código que enviasse a imagem para algum cloud da vida?​​

### Informações de suporte geral

1.  [Controllers 100% coesos](https://drive.google.com/file/d/10f3lT3lB2CEXdyss7ZjeSVzmDkzEU57d/view?usp=sharing) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://drive.google.com/file/d/1SMwN_Dd9MdWI047o5dGJuBdPygbc6giX/view?usp=sharing)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://drive.google.com/file/d/18Mu6IG0CzuDtTjoPsFJWscOxG2LZvv6O/view?usp=sharing).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://drive.google.com/file/d/1P_860b6FL8mIj9X8yyQyW4B2YNL2kW5V/view?usp=sharing) e depois [aqui](https://drive.google.com/file/d/1BgjdHCbrPP8ZuTRLi5tn2a7iPepr1sCR/view?usp=sharing)
5.  As imagens não são obrigatórias, mas quando o produto tem imagem associada é necessária que tenha pelo menos uma. Como você pode fazer para garantir que o produto, depois de ter imagens associadas, vai estar em um estado válido? Lembre da checagem de restrições. Você pode fazer uma verificação de estado do produto pós lógica de associação de imagens.
6.  Como você pode indicar que o produto precisa estar associado a no mínimo uma imagem? [que tal deixar uma dica para a outra pessoa](https://drive.google.com/file/d/1TMENbD2V_87FmEGzwjTb4zqUnucsDnKM/view?usp=sharing)?
7.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
8.  [Pegue cada uma das classes que você criou e realize a contagem da carga intrínseca](https://drive.google.com/file/d/1MwuEjVO9evwVsYK5t5hB0q22uHj7CwSQ/view?usp=sharing). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.
9.  Caso você já esteja utilizando um projeto de segurança. O framework da sua escolha, integrado com algum outro projeto de segurança, deve permitir que você tenha acesso ao objeto que representa o usuário logado dentro do método do seu controller. 
10.  Como Alberto faria esse código [parte1](https://drive.google.com/file/d/10X1RqlzWr6SvV0c60AyqKIc2FhLo4XNv/view?usp=sharing) e [parte 2(ownership)](https://drive.google.com/file/d/1XpX4SlTdEoTse_yc0u9dTPFyRU6zryyB/view?usp=sharing)

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