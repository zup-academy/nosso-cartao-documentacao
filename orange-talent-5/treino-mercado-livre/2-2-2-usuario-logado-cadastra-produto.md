# Usuário logado cadastra novo produto

### Explicação

Aqui a gente vai permitir o cadastro de um produto por usuário logado.

### Necessidades

*   Tem um nome
*   Tem um valor
*   Tem quantidade disponível
*   Características(cada produto pode ter um conjunto de características diferente). [Da uma olhada na parte de outras características nos detalhes de produtos do mercado livre](https://produto.mercadolivre.com.br/MLB-1279370191-bebedouro-bomba-eletrica-p-garrafo-galo-agua-recarregavel-_JM?variation=48969374724#reco_item_pos=0&reco_backend=navigation&reco_backend_type=function&reco_client=home_navigation-recommendations&reco_id=e55bf74a-9551-42d8-a43d-fb64fa3117d4&c_id=/home/navigation-recommendations/element&c_element_order=1&c_uid=761d5d17-5baf-4fd8-be79-fc65ee66a6fb). Cada característica tem um nome e uma descricao associada.
*   Tem uma descrição
*   Pertence a uma categoria
*   Instante de cadastro

### **Restrições**

*   Nome é obrigatório
*   Valor é obrigatório e maior que zero
*   Quantidade é obrigatório e >= 0
*   O produto possui pelo menos três características
*   Descrição é obrigatória e tem máximo de 1000 caracteres.
*   A categoria é obrigatória

### **Resultado esperado**

*   Um novo produto criado e status 200 retornado
*   Caso dê erro de validação retorne 400 e o json dos erros

### Antes de começar

Por favor descreva como você pretende realizar a implementação deste desafio. Para acessar o formulário [clique aqui](https://forms.gle/usXhgA628Pf3Ga8ZA)

### **Informações de suporte geral**

1.  [Controllers 100% coesos](https://youtu.be/NNKG2TFctfo) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://youtu.be/AzyHKZwNg1A)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://youtu.be/kzjSxBDQXp8).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://youtu.be/XPXOhvrJT1w) e depois [aqui](https://youtu.be/kkKqo80whqo)
5.  São muitas informações obrigatórias. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://youtu.be/NoKjl0xMt6w)
6.  Ainda na parte das informações obrigatórias tem aquela boa armadilha. Produto tem características, mas cada característica é de um produto. Como que você vai criar um sem o outro? Esse é um desafio muito bom. Resolvemos algo parecido no desafio da Casa do código. Só que tome cuidado, aqui precisa de menos engenharia :). 
7.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. Um email por exemplo. Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://youtu.be/iU19qJeXnVo)?
8.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
10.  Caso você já esteja utilizando um projeto de segurança. O framework da sua escolha, integrado com algum outro projeto de segurança, deve permitir que você tenha acesso ao objeto que representa o usuário logado dentro do método do seu controller. 
11.  Como Alberto faria esse código [parte 1​](https://youtu.be/dJRnTz7H96k) e [parte 2](https://youtu.be/ieXyWG-OC7Y) e [parte 3​](https://youtu.be/PxBySFg0bT8)
12. Como Alberto testaria o código dele? Confira em três partes: [PARTE 1](https://youtu.be/weQ1L_xUGZw), [PARTE 2](https://youtu.be/Q-X2Wfiecek) e [PARTE 3](https://drive.google.com/file/d/1Wr1yRfymAnaYTPzUQdVgG5K5pMEL8LY8/view?usp=sharing) :). 


### Informações de suporte para a combinação Java/Kotlin + Spring​

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/H6aM-4RaRrE)
5.  [Como externalizar as mensagens de erro no arquivo de configuração.](https://youtu.be/FO4HnZNCvoo)
6.  Use e abuse das annotations da bean validation para indicar as restrições dos parâmetros. ​
7.  Brinque um pouco com a classe **_Assert_**​ ​do Spring para fazer checagens de parâmetro também. As ideias de Design By Contract ajudam demais a aumentar a confiabilidade da aplicação. 
8.  Para configurar o Spring Security olhe [aqui](https://youtu.be/0I--CLsqC7w)​
9.  Lembrando que, para receber a referência para o usuário logado no método do controller, você pode usar a annotation _@AuthenticationPrincipal_​.

### Depois de finalizar

Antes de passar para a próxima funcionalidade, envie o link para o diff da sua solução acessando [este formulário](https://forms.gle/qqZe2v2ptMwV8SEE7)
