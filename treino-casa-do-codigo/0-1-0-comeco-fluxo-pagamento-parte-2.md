# Começo do fluxo de pagamento parte 2

## necessidades

Vamos receber também o parâmetro relativo ao carrinho de compras na requisição relativa aos dados da pessoa que está comprando. O json montado pelo cliente relativo ao carrinho tem o seguinte schema:

```
{
  "total": decimal,
  "itens":[
     {
      "idLivro":number,
      "quantidade": "number"
    },
     {
      "idLivro":number,
      "quantidade": "number"
    }
  ]
}
```

Reforçando aqui a explicação. A nossa aplicação da casa do código é divida em dois projetos. Temos a aplicação cliente e a aplicação que roda no backend. Neste cenário, toda lógica de construção do carrinho de compras ficou na aplicação cliente e, por conta disso, ela precisa enviar essa informação para o endpoint na mesma requisição que pegamos os dados da pessoa que estiver comprando. 


### restrição

* o total é não nulo
* o total é maior que zero
* tem pelo menos um item no carrinho
* idLivro é obrigatório
* idLivro precisa existir no banco de dados
* quantidade é obrigatória
* quantidade é maior que zero
* o total calculado no servidor precisa ser igual ao total enviado

### resultado esperado

* Em caso de tudo estar correto, uma nova compra deve ser gerada com todos os dados da pessoa que está comprando e também com as informações relativas ao carrinho de compras. No fim, retorne o status 201 com um endereço apontando onde os detalhes da compra podem ser encontrados.
* Em caso de falha de validação retorne 400

## sobre a utilização do material de suporte aqui

Estamos continuando o processo da criação de uma com​pra dentro do nosso sistema. Agora você tem um desafio de criar as classes que representam a estrutura do pedido. Tal estrutura está fora do seu controle, já que foi a aplicação responsável por controlar o carrinho de compras que decidiu. 

Existem alguns desafios para você nessa funcionalidade. Como você vai modelar o pedido? Como você vai verificar se o total especificado no json do carrinho realmente é o total relativo para aquele conjunto de itens?

## informações de suporte

* A prioridade máxima é funcionar de acordo com o caso de uso. Beleza e formosura não dão pão nem fartura. Isso não quer dizer que você deve fazer código com pressoa. Se ainda não está claro o que vai fazer, planeje um pouco. [Aqui tem um exemplo de planejamento](../informacao_suporte/planeje-um-pouco.md)

* Quando falamos de API existem vários métodos HTTP, qual se aplica ao cenário de criação de autor? [Aqui você encontra como fazer isso !!!](../informacao_suporte/rest-methods.md)

  * Ainda está com dúvida sobre qual método HTTP utilizar, não se preocupe! [Aqui você encontra como fazer isso !!!](../informacao_suporte/rest-post.md)

* Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [DÁ UMA OLHADA NESSE PILAR AQUI](../informacao_suporte/recebe-dados-requisicao.md).  

* Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [SUGIRO OLHAR UM POUCO SOBRE NOSSA IDEIA DE FORM VALUE OBJECTS](../informacao_suporte/conversao-para-dominio.md).

* Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele AQUI e depois [AQUI](../informacao_suporte/protegemos-as-bordas.md)

* Ainda sobre as bordas do sistema como se não houvesse amanhã. Caso você tenha criado um método no domínio para associar o cupom com a compra, como você fez para garantir que tal método só execute respeitando as restrições? Um pouco de [DESIGN BY CONTRACT](https://www.youtube.com/watch?v=4_5EfnU_oGs&feature=youtu.be)

* Utilize um insomnia ou qualquer outra forma para verificar o endpoint

* [PEGUE CADA UMA DAS CLASSES QUE VOCÊ CRIOU E REALIZE A CONTAGEM DA CARGA INTRÍNSECA](../informacao-suporte-design/treino-contagem-carga-intrinseca.md). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.

* [COMO ALBERTO FARIA ESSE CÓDIGO?](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/commit/a6e2b01d0ab6e8fded4bbd6f7a01cbfb79880a05)