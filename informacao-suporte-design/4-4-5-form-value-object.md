# Form Value Objects

Para assistir este conteúdo em vídeo, clique [aqui](https://drive.google.com/file/d/18Mu6IG0CzuDtTjoPsFJWscOxG2LZvv6O/view?usp=sharing)

​Por motivos de segurança e de fragilidade de contrato com as aplicações clientes, preferimos criar classes para representarem as requisições as informações que são enviadas em todo request. Este é inclusive um dos pilares de código que seguimos. 

Só que essas classes se enquadram na definição de classes inteligentes(aquelas que tem atributos de estado). Como elas são inteligentes, faz todo sentido tirarmos proveito da base orientação a objetos que é juntar comportamento com estado. Sendo mais antigo, juntar funções com variáveis contextualizadas para aquele conjunto de uma ou mais funções :). 

Neste cenário surge o que chamamos de **Form Value Objects**. ​Antes vistas apenas como classes de transferência de dados(DTO), elas já tinham sido vistas de forma diferente por Martin Fowler no que ele chamou de Local DTO. Justamente classes com atributos de estado mas que só seriam usadas para transferirem dados dentro da aplicação. Já um **Form Value Objects** é o que eu considero o reconhecimento da possibilidade de um Local DTO fazer mais. Se ele já tem atributo de dados, porque eu não vou operar sobre eles?