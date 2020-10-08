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

* Em caso de sucesso retorne 201
* Em caso de falha de validação retorne 400

## sobre a utilização do material de suporte aqui

Aqui você tem mais uma oportunidade de treinar uma operação similar a que você já encontrou. Essa é uma coisa que acontece regularmente na nossa vida trabalhando. Muitas vezes nos pegamos implementando códigos que já são mais usuais para a gente e achamos fácil. Achar fácil, ao contrário do que pode parecer é bom :). Quando está fácil, a chance é que você já tenha internalizado aquele conhecimento. E aí você pode se desafiar! Acha que é fácil? O quão rápido mantendo a qualidade você consegue fazer?

## informações de suporte

* Coloque um cronômetro, estime o tempo para fazer e desafie-se. 
* [COMO ALBERTO FARIA ESSE CÓDIGO?](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/commit/10837e178fbf0a55a75e68fa078683fbeeeae5c6)


