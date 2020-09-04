# Cadastro de cupom de desconto

## necessidades
A  cdc pode liberar cupons de desconto com valores e validade variados. Precisamos ter suporte a isso. 

Todo cupom tem:

* um código para ser entendido por pessoas
* um percentual de desconto
* uma validade para ser associado a uma compra

## restrições

* o código é obrigatório
* o código é único
* o percentual é obrigatório e positivo
* a validade é no futuro

## resultado esperado

* Em caso de sucesso retorne status 200
* Em caso de falha retorne status 400