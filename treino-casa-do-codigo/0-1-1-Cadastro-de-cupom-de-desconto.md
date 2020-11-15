# Cadastro de cupom de desconto

## **necessidades**

A cdc pode liberar cupons de desconto com valores e validade variados. Precisamos ter suporte a isso.

Todo cupom tem:

*   um código para ser entendido por pessoas
*   um percentual de desconto
*   uma validade para ser associado a uma compra

## **restrições**

*   o código é obrigatório
*   o código é único
*   o percentual é obrigatório e positivo
*   a validade é no futuro

## **resultado esperado**

*   status 400 e json de erros em caso de falha de validação
*   status 200 e cupom gerado

## **sobre a utilização do material de suporte aqui**

Mais um cadastro para você treinar​ as práticas que temos feito. Tente fazer sozinho(a).

## **informações de suporte para a feature**

1.  [Como Alberto faria esse código?](https://drive.google.com/file/d/1cjs9cV6lDPZQhzDIuTvuJZhMruAYZuZH/view?usp=sharing)
