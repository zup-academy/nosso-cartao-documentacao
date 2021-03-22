# Usuário logado adiciona imagem no seu produto

### Explicação

Com um produto cadastrado, um usuário logado pode adicionar imagens ao seu produto. Não precisa salvar a imagem em algum cloud ou no próprio sistema de arquivos. Cada arquivo de imagem pode virar um link ficticio que pode ser adicionado ao produto. 

### **Necessidades**

*  Adicionar uma ou mais imagens a um determinado produto do próprio usuário

### **Restrições**

*  Tem uma ou mais fotos
*  Só pode adicionar fotos ao produto que pertence ao próprio usuário

### Resultado esperado

*   Imagens adicionadas e 200 como retorno
*   Caso dê erro de validação retorne 400 e o json dos erros
*   Caso tente adicionar imagens a um produto que não é seu retorne 403.

### Antes de começar
Por favor descreva como você pretende realizar a implementação deste desafio. Para acessar o formulário [clique aqui](https://forms.gle/wf8Gk2mp22Hd1MCQA)

### Desafio extra

Como você faria para que em dev a imagem virasse um link fictício e em produção executasse um código que enviasse a imagem para algum cloud da vida?​​

### Informações de suporte geral

1.  [Controllers 100% coesos](https://youtu.be/NNKG2TFctfo) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://youtu.be/AzyHKZwNg1A)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://youtu.be/kzjSxBDQXp8).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://youtu.be/XPXOhvrJT1w) e depois [aqui](https://youtu.be/kkKqo80whqo)
5.  As imagens não são obrigatórias, mas quando o produto tem imagem associada é necessária que tenha pelo menos uma. Como você pode fazer para garantir que o produto, depois de ter imagens associadas, vai estar em um estado válido? Lembre da checagem de restrições. Você pode fazer uma verificação de estado do produto pós lógica de associação de imagens.
6.  Como você pode indicar que o produto precisa estar associado a no mínimo uma imagem? [que tal deixar uma dica para a outra pessoa](https://youtu.be/iU19qJeXnVo)?
7.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
9.  Caso você já esteja utilizando um projeto de segurança. O framework da sua escolha, integrado com algum outro projeto de segurança, deve permitir que você tenha acesso ao objeto que representa o usuário logado dentro do método do seu controller. 
10.  Como Alberto faria esse código [parte1](https://youtu.be/vwPOO1LPfIc) e [parte 2(ownership)](https://youtu.be/HaiLyPBhAxo)

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

### Depois de finalizar

Antes de passar para a próxima funcionalidade, envie o link para o diff da sua solução acessando [este formulário](https://forms.gle/7Ur27NGnzjQpdzGN9)

