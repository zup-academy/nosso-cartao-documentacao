### Modelando um recurso REST

Existem um conjunto de boas práticas para fazer um bom design de API, vamos explorar
algumas práticas na criação de um path de uma **API**. 

**Path API**

http://servidor/carrinhos/efa3df09-366b-4d85-9c10-b5244ffb35a9/itens/fbcc35b6-b02b-4f74-a992-7a4d6a84d10f

#### Vamos entender um pouco dessa URL

**Recurso**

_/carrinhos_

Coleções dos elementos sempre no plural, procure criar recursos que tenham algum sentido para o negócio e seja
fácil de ser identificado num contexto de negócio. Por exemplo num contexto de _ecommerce_ carrinho é um substantivo
bastante familiar a todos os participantes envolvidos no sistema.
Sugestão podemos usar alguns conceitos do [DDD - Domain Driven Design](https://www.infoq.com/br/news/2019/07/bounded-context-eric-evans/) na modelagem aqui!!


**Identificador do recurso**

_efa3df09-366b-4d85-9c10-b5244ffb35a9_

Identificador do carrinho nosso recurso principal. Esse identificador deve ser único em todo o sistema.
Procure utilizar [UUIDs](https://pt.wikipedia.org/wiki/Identificador_%C3%BAnico_universal) isso adiciona uma camada de segurança evitando que o atacante não consiga "prever"
o próximo elemento da coleção, essa característica traz um pouco de imprevisibilidade.  

**Sub Recurso**

_itens_

Sub Recurso do carrinho, neste caso o carrinho possui itens.
Aqui temos um sub-recurso, temos uma relação de pai-filho nesse caso, um item de carrinho sempre vai
pertencer à um carrinho não há motivo para um item não estar em um carrinho.

**Identificador do sub recurso**

_fbcc35b6-b02b-4f74-a992-7a4d6a84d10f_

Identificador de um item do carrinho.Podemos usar UUIDs caso você deseje adicionar
característica de imprevisibilidade, ou aqui podemos usar o identificador sequencial que não há problemas 

#Informação de Suporte

Quer aprender sobre como modelar Status Codes, [Veja Aqui !!!](../informacao_procedural/rest.md)
