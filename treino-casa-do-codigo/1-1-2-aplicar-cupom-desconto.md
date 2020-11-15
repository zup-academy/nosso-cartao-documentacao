# Aplicar cupom de desconto na compra

## **necessidades**

Agora, no começo do processo de finalização de compra, um cupom pode ser aplicado.

Lembrando, a informação do cupom vai junto com as informação da pessoa que está comprando e carrinho de compras.

## **restrições**

*   o código do cupom precisa ser válido
*   o cupom precisa ser válido ainda
*   uma vez associado o cupom, uma compra nunca pode ter essa informação alterada.
*   O cupom só pode ser associada com uma compra que ainda não foi registrada no banco de dados (esse daqui eu não implementei)

## **resultado esperado**

Manter o mesmo resultado que já existia

### sobre a utilização do material de suporte aqui

Agora você tem mais um passo para fazer no momento da criação da compra, que é a aplicação do cupom. A verdade é que você já treinou tudo que precisa para implementar essa funcionalidade.

## **informações de suporte para a feature**

1.  A prioridade do código é funcionar([parte 1](https://drive.google.com/file/d/1yZIhgjrV5HghcDSvIKmNaWF5FKAgcWS9/view?usp=sharing) e [parte2](https://drive.google.com/file/d/10QO8jZJ2WTIJFCJ2-1iyQxAH7YmxiOX5/view?usp=sharing)). Lembre que é bem importante você investir alguns minutos planejando como que a funcionalidade será feita. 
2.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://drive.google.com/file/d/1SMwN_Dd9MdWI047o5dGJuBdPygbc6giX/view?usp=sharing)
3.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://drive.google.com/file/d/18Mu6IG0CzuDtTjoPsFJWscOxG2LZvv6O/view?usp=sharing).
4.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://drive.google.com/file/d/1P_860b6FL8mIj9X8yyQyW4B2YNL2kW5V/view?usp=sharing) e depois [aqui](https://drive.google.com/file/d/1BgjdHCbrPP8ZuTRLi5tn2a7iPepr1sCR/view?usp=sharing)
5.  Ainda sobre as bordas do sistema como se não houvesse amanhã. Caso você tenha criado um método no domínio para associar o cupom com a compra, como você fez para garantir que tal método só execute respeitando as restrições? Um pouco de [Design by Contract](https://youtu.be/4_5EfnU_oGs)
7.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
8.  [Como Alberto faria esse código?](https://drive.google.com/file/d/1cTj--WlyMGBgO2TWlo533fJInGWUM4Fv/view?usp=sharing)