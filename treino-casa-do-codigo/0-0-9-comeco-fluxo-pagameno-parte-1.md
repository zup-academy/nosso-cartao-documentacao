# Começo do fluxo de pagamento

## necessidades
Uma coisa importante. Na cdc, você não faz um cadastro e tem suas compras associadas. Toda vez você coloca seu email, cpf etc. Como isso vai ser implementado depende da aplicação.

Os seguintes campos precisam ser preenchidos:

* email
* nome
* sobrenome
* documento(cpf/cnpj)
* endereco
* complemento
* cidade
* país
* estado(caso aquele pais tenha estado)
* telefone
* cep

### restrição

* email obrigatório e com formato adequado
* nome obrigatório
* sobrenome obrigatório
* documento(cpf/cnpj) obrigatório e só precisa ser um cpf ou cnpj
* endereco obrigatório
* complemento obrigatório
* cidade obrigatório
* país obrigatório
* estado (apenas se o país tiver cadastro de estados)
* telefone obrigatório
* cep é obrigatório

### resultado esperado

* Aqui ainda estamos no meio do processo. Então no final desta etapa você precisa ter um endpoint criado recebendo os dados da pessoa que está comprando e com os dados validados. Retorne 201 em caso de sucesso.
* Em caso de falha de validação retorne status 400

## sobre a utilização do material de suporte aqui

Este começo de fechamento de compra envolve muitos passos. Decidimos começar pegando apenas os dados do formulário relativo a pessoa que está comprando. Este é um formulário um pouco mais desafiador, já que possuímos algumas validações customizadas que precisam ser feitas. Não tem nada que você não tenha trabalhado até aqui, mas é mais uma chance de você treinar sua habilidade para conhecer mais das tecnologias e colocar em prática alguns dos pilares que vem nos norteando. ​

## informações de suporte

* A prioridade máxima é funcionar de acordo com o caso de uso. Beleza e formosura não dão pão nem fartura. Isso não quer dizer que você deve fazer código com pressoa. Se ainda não está claro o que vai fazer, planeje um pouco. [Aqui tem um exemplo de planejamento](../informacao_suporte/planeje-um-pouco.md)

* Quando falamos de API existem vários métodos HTTP, qual se aplica ao cenário de criação de autor? [Aqui você encontra como fazer isso !!!](../informacao_suporte/rest-methods.md)

  * Ainda está com dúvida sobre qual método HTTP utilizar, não se preocupe! [Aqui você encontra como fazer isso !!!](../informacao_suporte/rest-post.md)

* [CONTROLLERS 100% COESOS](../informacao-suporte-design/controllers-100-coesos.md) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.

* Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [DÁ UMA OLHADA NESSE PILAR AQUI](../informacao_suporte/recebe-dados-requisicao.md).

* Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [SUGIRO OLHAR UM POUCO SOBRE NOSSA IDEIA DE FORM VALUE OBJECTS](../informacao_suporte/conversao-para-dominio.md).

* Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [AQUI](../informacao_suporte/protegemos-as-bordas.md)

* [FAVORECEMOS A COESÃO ATRAVÉS DO ENCAPSULAMENTO.](https://medium.com/@albertosouza_47783/encapsulamento-sob-uma-perspectiva-l%C3%B3gica-3d04016e3f14) Como você planeja validar se o documento é válido?

* Utilize um insomnia ou qualquer outra forma para verificar o endpoint

* [PEGUE CADA UMA DAS CLASSES QUE VOCÊ CRIOU E REALIZE A CONTAGEM DA CARGA INTRÍNSECA](../informacao-suporte-design/treino-contagem-carga-intrinseca.md). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.

* [COMO ALBERTO FARIA ESSE CÓDIGO?](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/commit/57533ae6afd88dde4533bdd6bc02d09d7c18d1f7)



