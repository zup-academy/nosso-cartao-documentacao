## Um cenário de integração com um serviço externo

Em um projeto que simula a API necessária para servir um cartão de crédito, temos o processo de criação de uma nova proposta e sua posterior aprovação por um sistema externo. O contrato do serviço externo diz que ele pode retornar uma das duas Strings abaixo:

* SEM_RESTRICAO
* COM_RESTRICAO

Com essas informações em maos, o fluxo da criação de uma proposta pode ser mais ou menos o seguinte:

```java
    Proposta novaProposta = //cria nova proposta;
    //aqui estamos simulando uma consulta ao sistema externo via post por motivos de segurança
    String resultadoAvaliacao = requisicao.post(endereco).body(novaProposta.getDocumento()).execute();

    novaProposta.setStatus(resultadoAvaliacao);

```

Agora, o método ```setStatus``` da classe ```Proposta``` pode ser algo parecido com o que segue:

```java
    public void setStatus(String resultadoAvaliacao){
        this.resultadoAvaliacao = resultadoAvaliacao;
    }
```

## Algumas vezes um tipo básico vem carregado de semântica

Quando a gente implementa um código como o de cima é criado um dos piores tipo de acoplamento que podemos ter no software. Aquele que não é pego em tempo de compilação e vive dentro da nossa cabeça. Quem implementou o ```setStatus``` sabe que este método está sendo invocado a partir do ponto de criação de uma nova proposta e também sabe que, daquele ponto, só podem vir duas variações de ```String```. 

Agora, se você fizer o exercício de olhar apenas para o método ```setStatus```, como que alguém pode saber que ali só podem chegar dois tipos de valores diferentes? Não existe meio para que isso aconteça. Estamos um tipo definido previamente definido pela linguagem para representar algo que vem carregado de semântica. 

Ainda fazendo o exercício de olhar apenas para o método ```setStatus```, a implementação mostra que ele acredita que toda ```String``` vai ser válida, o que também não pode ser afirmado se você olhar só para este contexto. Um dos ensinamentos do Design By Contract é que a gente a gente sempre verifica se os parâmetros atendem as restrições de uso para o funcionamento correto do método/função. *Protegemos as bordas do sistema como se não houvesse amanhã*

Tipos padrões carregados de semântica podem acontecer em diversas situações diferentes:

* Um inteiro que representa um range;
* Uma String que representa uma senha que deveria estar encodada;
* Uma String que representa um email;

A solução para todas as questões parecidas com essa infelizmente não é sempre a mesma, devido a limitações da linguagem Java e das outras linguagens utilizadas regularmente dentro da indústria de desenvolvimento.


## Ideias de solução

Agora que tentamos deixar claro algumas situações onde os tipos padrões vem carregados de semântica, é importante buscar ideias para amenizar o impacto disso na manutenção do código. Algumas coisas que você pode pensar:

* Posso substituir por alguma estrutura já pronta da linguagem? Criar enums?
* Posso criar uma classe intermediária que talvez tenha métodos que tentem dar uma dica do que está sendo feito?
* Deixo também um comentário no código para tentar sinalizar o que é esperado de entrada?

Um ponto de atenção na solução é que toda criação de classe tende a aumentar a complexidade do código como um todo, por mais que possa facilitar aquele ponto específico de entendimento. É um equilíbrio que precisamos sempre buscar.