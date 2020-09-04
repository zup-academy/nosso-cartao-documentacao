# Cadastro de país e estados

## Contexto

Estamos chegando na fase de receber os dados da pessoa que está comprando dentro da casa do código e, nessa fase, vamos precisar do país e do estado daquela pessoa. 

Existe apenas um detalhe que para alguns países o sistema da casa do código não registra país. Podemos ter N países, mas nem todos os países tem estados.

## necessidades
* Precisamos de um cadastro simples de países.
* Precisamos de um cadastro de estados para os países que tem estados.

Cada país tem um nome e cada estado, quando cadastrado, tem um nome e pertence a um país. 

## restrições para país

* o nome é obrigatório
* o nome é único

## restrição para estados

* o nome é obrigatório
* o nome é único
* o id do país é obrigatório
* o id do país precisa existir no banco de dados

## detalhe importante

São dois endpoints diferentes.

## resultado esperado

* Em caso de sucesso retorne 200
* Em caso de falha de validação retorne 400