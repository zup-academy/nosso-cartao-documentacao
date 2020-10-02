# Criar um novo livro

## necessidades

* Um título
* Um resumo do que vai ser encontrado no livro
* Um sumário de tamanho livre. O texto deve entrar no formato markdown, que é uma string. Dessa forma ele pode ser formatado depois da maneira apropriada.
* Preço do livro
* Número de páginas
* Isbn(identificador do livro)
* Data que ele deve entrar no ar(de publicação)
* Um livro pertence a uma categoria
* Um livro é de um autor

## restrições

* Título é obrigatório
* Título é único
* Resumo é obrigatório e tem no máximo 500 caracteres
* Sumário é de tamanho livre. 
* Preço é obrigatório e o mínimo é de 20
* Número de páginas é obrigatória e o mínimo é de 100
* Isb é obrigatório, formato livre
* Isbn é único
* Data que vai entrar no ar precisa ser no futuro
* O id da categoria é obrigatório
* O id da categoria precisa existir no banco de dados
* O id do autor é obrigatório
* O id do autor precisa existir no banco de dados

## resultado esperado
* Em caso de sucesso retorne 200
* Em caso de falha de validação retorne 400

## informações de suporte

* A prioridade máxima é funcionar de acordo com o caso de uso. Beleza e formosura não dão pão nem fartura. Isso não quer dizer que você deve fazer código com pressa. Se ainda não está claro o que vai fazer, planeje um pouco. [Aqui tem um exemplo de planejamento](../informacao_suporte/planeje-um-pouco.md)

* Quando falamos de API existem vários métodos HTTP, qual se aplica ao cenário de criação de autor? [Aqui você encontra como fazer isso !!!](../informacao_suporte/rest-methods.md)

  * Ainda está com dúvida sobre qual método HTTP utilizar, não se preocupe! [Aqui você encontra como fazer isso !!!](../informacao_suporte/rest-post.md)

* [CONTROLLERS 100% COESOS](../informacao-suporte-design/controllers-100-coesos.md) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.

* Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [DÁ UMA OLHADA NESSE PILAR AQUI](../informacao_suporte/recebe-dados-requisicao.md).

* Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [SUGIRO OLHAR UM POUCO SOBRE NOSSA IDEIA DE FORM VALUE OBJECTS](../informacao_suporte/conversao-para-dominio.md).

* Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele AQUI e depois [AQUI](../informacao_suporte/protegemos-as-bordas.md)

* O livro tem muitas informações obrigatórias. Aqui a palavra chave é **obrigatoriedade**. Como você lidou com isso?[INFORMAÇÃO NATURAL E OBRIGATÓRIA ENTRA PELO CONSTRUTOR](../informacao-suporte-design/construtor-para-informacao-natural.md)

* Um construtor com muitos argumentos de tipo parecido pode gerar dificuldade para uma pessoa acertar a ordem dos parâmetros. Que tal você olhar para um pattern escrito no livro Design Patterns chamado Builder? Será que vale a pena utilizá-lo?
 * Caso você tenha ouvido falar do Lombok, é importante saber que o Builder fornecido por ele quebra a regra "informação natural entra pelo construtor". **Não recomendamos usar.** 

* Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. Um email por exemplo. Se você não pode garantir a validação do formato em compilação, [QUE TAL DEIXAR UMA DICA PARA A OUTRA PESSOA?](../informacao-suporte-design/deixe-pistas-para-as-pessoas.md)

* Lembre que aqui você precisa receber uma data como argumento e, em geral, o seu framework não vai saber automaticamente qual formato ele deve se basear para pegar o texto e transformar para um objeto que represente a data em si na sua linguagem. Você deve precisar configurar.

* Utilize um insomnia ou qualquer outra forma para verificar o endpoint

* [PEGUE CADA UMA DAS CLASSES QUE VOCÊ CRIOU E REALIZE A CONTAGEM DA CARGA INTRÍNSECA](../informacao-suporte-design/treino-contagem-carga-intrinseca.md). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.

* [COMO ALBERTO FARIA ESSE CÓDIGO?](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/commit/ad06e72efe9ac775667936a736e3ce633c408d02)

## informações extras de suporte

* Se você tiver um atributo do tipo LocalDate,LocalDateTime etc e tiver recebendo os dados como JSON, vai precisar usar a annotation ```@JsonFormat(pattern = "padrao da data aqui", shape = Shape.STRING)​```

* Se você tiver recebendo os dados da maneira tradicional, ou seja via form-url-encoded vai precisar usar a annotation ```@DateTimeFormat```

* Para receber os dados da request como json, temos a annotation ```@RequestBody```

* Usamos a annotation ```@Valid``` para pedir que os dados da request sejam validados

* Está pensando em como fazer as validações dos dados do seu objeto? Olha que interessante, já existe um especificação no mundo Java que pensou só nisso. Ela é chamada Bean Validation. Inclusive o Spring já tem integração fina com ela. [Confere essa dica aqui](../informacao_suporte/bean-validation.md)

* [COMO CRIAR UM @RESTCONTROLLERADVICE PARA CUSTOMIZAR O JSON DE SAÍDA COM ERROS DE VALIDAÇÃO](../informacao_suporte/error-spring.md)

* [Exemplo de um ```RestControllerAdvice``` para você utilizar.](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/blob/master/src/main/java/com/deveficiente/casadocodigov2/compartilhado/ValidationErrorHandler.java) 

* [COMO EXTERNALIZAR AS MENSAGENS DE ERRO NO ARQUIVO DE CONFIGURAÇÃO](../informacao_suporte/externaliza-mensagens-properties.md)

## sensações

Aqui, mesmo com muito mais informações, você deve ter tido de novo um pouco daquele sentimento robótico. E aí a gente se questiona, mas não é um trabalho criativo? Não o tempo todo. Não só em desenvolvimento de software, como em qualquer outro trabalho considerado criativo, os momentos onde você vai realmente precisa combinar conhecimentos de uma forma diferente para sair com uma solução da cartola são escassos. O que você precisa estar é preparado(a)! 

O código estar ficando mais fácil é um sinal que você está dominando mais as habilidades necessárias para fazer api's web, o framework, a linguagem etc. Quando aparecer uma funcionalidade mais complicada, você vai ter mais chance de performar melhor.
