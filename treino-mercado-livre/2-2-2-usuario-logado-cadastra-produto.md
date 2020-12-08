# Usuário logado cadastra novo produto

### Explicação

Aqui a gente vai permitir o cadastro de um produto por usuário logado.

### Necessidades

*   Tem um nome
*   Tem um valor
*   Tem quantidade disponível
*   Características(cada produto pode ter um conjunto de características diferente). [Da uma olhada na parte de outras características nos detalhes de produtos do mercado livre](https://produto.mercadolivre.com.br/MLB-1279370191-bebedouro-bomba-eletrica-p-garrafo-galo-agua-recarregavel-_JM?variation=48969374724#reco_item_pos=0&reco_backend=navigation&reco_backend_type=function&reco_client=home_navigation-recommendations&reco_id=e55bf74a-9551-42d8-a43d-fb64fa3117d4&c_id=/home/navigation-recommendations/element&c_element_order=1&c_uid=761d5d17-5baf-4fd8-be79-fc65ee66a6fb). Cada característica tem um nome e um valor associado.
*   Tem uma descrição
*   Pertence a uma categoria
*   Instante de cadastro

### **restrições**

*   Nome é obrigatório
*   Valor é obrigatório e maior que zero
*   Quantidade é obrigatório e >= 0
*   O produto possui pelo menos três características
*   Descrição é obrigatória e tem máximo de 1000 caracteres.
*   A categoria é obrigatória

### **resultado esperado**

*   Um novo produto criado e status 200 retornado
*   Caso dê erro de validação retorne 400 e o json dos erros

### **informações de suporte geral**

1.  [Controllers 100% coesos](https://drive.google.com/file/d/10f3lT3lB2CEXdyss7ZjeSVzmDkzEU57d/view?usp=sharing) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://drive.google.com/file/d/1SMwN_Dd9MdWI047o5dGJuBdPygbc6giX/view?usp=sharing)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://drive.google.com/file/d/18Mu6IG0CzuDtTjoPsFJWscOxG2LZvv6O/view?usp=sharing).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://drive.google.com/file/d/1P_860b6FL8mIj9X8yyQyW4B2YNL2kW5V/view?usp=sharing) e depois [aqui](https://drive.google.com/file/d/1BgjdHCbrPP8ZuTRLi5tn2a7iPepr1sCR/view?usp=sharing)
5.  São muitas informações obrigatórias. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://drive.google.com/file/d/1988eYtK-AqS6FVET1zO04HzjM6egHoKM/view?usp=sharing)
6.  Ainda na parte das informações obrigatórias tem aquela boa armadilha. Produto tem características, mas cada característica é de um produto. Como que você vai criar um sem o outro? Esse é um desafio muito bom. Resolvemos algo parecido no desafio da Casa do código. Só que tome cuidado, aqui precisa de menos engenharia :). 
7.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. Um email por exemplo. Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://drive.google.com/file/d/1TMENbD2V_87FmEGzwjTb4zqUnucsDnKM/view?usp=sharing)?
8.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
10.  Caso você já esteja utilizando um projeto de segurança. O framework da sua escolha, integrado com algum outro projeto de segurança, deve permitir que você tenha acesso ao objeto que representa o usuário logado dentro do método do seu controller. 
11.  Como Alberto faria esse código [parte 1​](https://drive.google.com/file/d/1ivcB_pHIfAaEzpct8D6sp5mBTDL2zNLf/view?usp=sharing) e [parte 2](https://drive.google.com/file/d/1pV3i5TpGPUNoLBbf9HkcUF60x5vPKZV0/view?usp=sharing) e [parte 3​](https://drive.google.com/file/d/1kZ-HJKYdfN_49j8X-MYMLH0xJnixwJpr/view?usp=sharing)
12. Como Alberto testaria o código dele? Confira em três partes: [PARTE 1](https://drive.google.com/file/d/10Ufz_v8SmbdKie7Yxn7EW-dOgWCpqB-n/view?usp=sharing), [PARTE 2](https://drive.google.com/file/d/1Wr1yRfymAnaYTPzUQdVgG5K5pMEL8LY8/view?usp=sharing) e [PARTE 3](https://drive.google.com/file/d/1Wr1yRfymAnaYTPzUQdVgG5K5pMEL8LY8/view?usp=sharing) :). 


### informações de suporte para a combinação Java/Kotlin + Spring​

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://drive.google.com/file/d/18q7IUF1EmeGrPFAab1CHIXP3COf5KNHd/view?usp=sharing)
5.  [Como externalizar as mensagens de erro no arquivo de configuração.](mailto:Como%20criar%20um%20@RestControllerAdvice%20para%20customizar%20o%20json%20de%20sa%C3%ADda%20com%20erros%20de%20valida%C3%A7%C3%A3o)
6.  Use e abuse das annotations da bean validation para indicar as restrições dos parâmetros. ​
7.  Brinque um pouco com a classe **_Assert_**​ ​do Spring para fazer checagens de parâmetro também. As ideias de Design By Contract ajudam demais a aumentar a confiabilidade da aplicação. 
8.  Para configurar o Spring Security olhe [aqui](https://drive.google.com/file/d/1314vY4OpQqTPAnb5fPaMCaWEYdZqpP78/view?usp=sharing)​
9.  Lembrando que, para receber a referência para o usuário logado no método do controller, você pode usar a annotation _@AuthenticationPrincipal_​.