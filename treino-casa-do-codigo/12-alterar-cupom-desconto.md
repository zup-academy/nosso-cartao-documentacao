# Alterar cupom de desconto

## necessidades

Pode existir a necessidade de alterar um cupom de desconto. As informações que podem ser alteradas são as seguintes:

* Data de validade
* Percentual de desconto
* Código

## restrições

* o código é obrigatório
* o código é único
* o percentual é obrigatório e positivo
* a validade é no futuro

## resultado esperado

* Em caso de sucesso retorne status 200
* Em caso de falha retorne status 400