# Começo do fluxo de pagamento parte 2

### **necessidades**

Receber também o parâmetro relativo ao carrinho de compras no formulário final. O json montado pelo cliente relativo ao carrinho tem o seguinte formato:

```
{
  total": decimal,
  "itens":[
     {
      "idLivro":number,
      "quantidade": "number"
    },
     {
      "idLivro":number,
      "quantidade": number
    }
  ]
}
```
Importante ressaltar que essa atividade é uma continuação da anterior. Na mesma requisição que vem os dados da pessoa que está comprando, também vem os dados relativos ao carrinho de compras.

### **restrição**

*   o total é não nulo
*   o total é maior que zero
*   tem pelo menos um item no carrinho
*   idLivro é obrigatório e precisa existir
*   quantidade é obrigatória
*   quantidade é maior que zero
*   o total calculado no servidor precisa ser igual ao total enviado

### **resultado esperado**

*   Compra gerada com um status de iniciada
*   status 201 gerado com o endereço de detalhe da compra

### sobre a utilização do material de suporte aqui

Estamos continuando o processo da criação de uma com​pra dentro do nosso sistema. Agora você tem um desafio de criar as classes que representam a estrutura do pedido. Tal estrutura está fora do seu controle, já que foi a aplicação responsável por controlar o carrinho de compras que decidiu. 

Existem alguns desafios para você nessa funcionalidade. Como você vai modelar a ideia do carrinho de compras? Como você vai verificar se o total especificado no json do carrinho realmente é o total relativo para aquele conjunto de itens? 

### **informações de suporte para a feature**

1.  A prioridade do código é funcionar([aqui](https://drive.google.com/file/d/1yZIhgjrV5HghcDSvIKmNaWF5FKAgcWS9/view?usp=sharing) e [aqui](https://drive.google.com/file/d/10QO8jZJ2WTIJFCJ2-1iyQxAH7YmxiOX5/view?usp=sharing)). Isso não significa que você precisa ter pressa e sair implementando sem refletir. Dessa forma você aumenta as chances de ter que ficar reescrevendo o código. O código começa a ter mais chances de funcionar na hora do planejamento. Lembre que é bem importante você investir alguns minutos planejando como que a funcionalidade será feita. 
2.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://drive.google.com/file/d/18Mu6IG0CzuDtTjoPsFJWscOxG2LZvv6O/view?usp=sharing).
3.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://drive.google.com/file/d/1P_860b6FL8mIj9X8yyQyW4B2YNL2kW5V/view?usp=sharing) e depois [aqui](https://drive.google.com/file/d/1BgjdHCbrPP8ZuTRLi5tn2a7iPepr1sCR/view?usp=sharing)
4.  Uma compra tem muita informação obrigatória. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://drive.google.com/file/d/1988eYtK-AqS6FVET1zO04HzjM6egHoKM/view?usp=sharing)
5.  Ainda sobre as informações obrigatórias. Talvez você tenha uma armadilha entre a relação do pedido e a compra. Uma compra tem pedido, mas o pedido é de uma compra. Como fazer para manter a restrição?. [Aqui](https://youtu.be/dgNx-V4pMeE) tem um vídeo gravado sobre esse dilema(assista se achar pertinente)
6.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. Um email por exemplo. Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://drive.google.com/file/d/1TMENbD2V_87FmEGzwjTb4zqUnucsDnKM/view?usp=sharing)? De novo aqui temos um construtor complicado. Será que queremos um builder? 
7.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://drive.google.com/file/d/1wc5ChsPeGFjqypb9QI7tGRMl9dn0WkkL/view?usp=sharing)
8.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
9.  Como Alberto faria esse código? ([Parte 1](https://drive.google.com/file/d/15uvJm9l2oYW60RLY1IwyEZ1qYQHqXGm9/view?usp=sharing) e [Parte2](https://drive.google.com/file/d/15bb5uLjyJwSXgctKiCgf8Eyy1CIxWr0K/view?usp=sharing))​