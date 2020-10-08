# Cadastro de uma categoria

## necessidades

* Toda categoria precisa de um nome

## restrições

* O nome é obrigatório
* O nome não pode ser duplicado

## resultado esperado
* Em caso de sucesso retorne 201
* Em caso de falha de validação retorne 400

## informações de suporte

* A prioridade máxima é funcionar de acordo com o caso de uso. Beleza e formosura não dão pão nem fartura. Isso não quer dizer que você deve fazer código com pressoa. Se ainda não está claro o que vai fazer, planeje um pouco. [Aqui tem um exemplo de planejamento](../informacao_suporte/planeje-um-pouco.md)

* Quando falamos de API existem vários métodos HTTP, qual se aplica ao cenário de criação de autor? [Aqui você encontra como fazer isso !!!](../informacao_suporte/rest-methods.md)

  * Ainda está com dúvida sobre qual método HTTP utilizar, não se preocupe! [Aqui você encontra como fazer isso !!!](../informacao_suporte/rest-post.md)

* [CONTROLLERS 100% COESOS](../informacao-suporte-design/controllers-100-coesos.md) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.

* Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [DÁ UMA OLHADA NESSE PILAR AQUI](../informacao_suporte/recebe-dados-requisicao.md).

* Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [SUGIRO OLHAR UM POUCO SOBRE NOSSA IDEIA DE FORM VALUE OBJECTS](../informacao_suporte/conversao-para-dominio.md).

* Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele AQUI e depois [AQUI](../informacao_suporte/protegemos-as-bordas.md)

* Nome é obrigatório. Como você lidou com isso? [INFORMAÇÃO NATURAL E OBRIGATÓRIA ENTRA PELO CONSTRUTOR](../informacao-suporte-design/construtor-para-informacao-natural.md)

* [TODO FRAMEWORK MVC MINIMAMENTE MADURO POSSUI UM MECANISMO PRONTO DE REALIZAR VALIDAÇÃO CUSTOMIZADA. SPRING, NESTJS E ASP.NET CORE MVC TÊM](../informacao-suporte-design/validacao-precisa-ser-suportada-fw.md).


* Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. O nome aqui é obrigatório, mas você não consegue garantir isso em tempo de compilação. Se você não pode garantir a validação do formato em compilação, [QUE TAL DEIXAR UMA DICA PARA A OUTRA PESSOA?](../informacao-suporte-design/deixe-pistas-para-as-pessoas.md)

* Utilize um insomnia ou qualquer outra forma para verificar o endpoint

* [PEGUE CADA UMA DAS CLASSES QUE VOCÊ CRIOU E REALIZE A CONTAGEM DA CARGA INTRÍNSECA](../informacao-suporte-design/treino-contagem-carga-intrinseca.md). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.

* [COMO ALBERTO FARIA ESSE CÓDIGO?](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/commit/3670e63786b0029cc7fb596c57d285e002717490)
 * Alberto deixou a solução de nome único para a outra funcionalidade :). 

## sensações

Talvez aqui você tenha achado que o código foi até meio repetitivo. E a verdade é que foi mesmo. Talvez no próximo você ache que foi até meio robótico, vai ser melhor ainda. Quanto mais automático você sente que é para fazer algo quer dizer que mais dominado aquilo está. O que você precisa sempre se questionar é: Será que este padrão ​ainda pode melhorar? Não é para buscar a melhoria de forma maluca, apenas para estar alerta em relação as próprias decisões.
