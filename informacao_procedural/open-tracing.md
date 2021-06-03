# OpenTracing

Nos últimos anos os modelos de arquitetura distribuídos, como o Microsserviços, vem sendo amplamente adotadas pelas empresas 
por prover vários benefícios para as mesmas. Porém como tudo em tecnologia, temos vantagens e desvantagens!

Uma desvantagem bastante latente nesse estilo de arquitetura é o troubleshooting de problemas: quanto mais serviços, 
maior será a complexidade de encontrar a causa raiz do problema, como por exemplo na imagem abaixo:

![alt text](../images/open-tracing-001.png "OpenTracing")

Na imagem acima uma chamada HTTP, pode se tornar várias chamadas internas, aumentando os pontos de falhas! Quando ocorrer 
um erro, como saber qual chamada interna falhou e como descobrir isso de forma efetiva?

Uma alternativa é coletar os logs de cada serviço e analisá-los. Num cenário onde temos poucos serviços isso parece 
viável, mas e quando tiver inúmeras instâncias desse um mesmo serviço sendo executadas? Imagina que  no exemplo da
figura acima tenhamos 5 instâncias de cada serviço. Logo, teríamos que coletar e analisar logs de 20 instâncias diferentes.
Para dificultar ainda mais o trabalho, lembramos que os logs possuem informações sobre as diversas requisições que as
instâncias dos serviços estão processando, e não somente as que estamos buscando. 

Não parece ser viável e eficaz!

Visando resolver esses problemas a comunidade iniciou o desenvolvimento de soluções para melhorar a observabilidade dos nossos serviços, 
como por exemplo:

- Trace
- Métricas
- Logs

Assim foi criada a especificação do OpenTracing para tratar do pilar de Trace. A ideia consiste em gerar metadados no início
de cada operação para identificá-las, e propagá-los internamente entre os serviços envolvidos na operação podendo ser 
utilizado quaisquer protocolos que implementam a especificação, como por exemplo:

- HTTP
- AMQP
- RPC

Com base nos metadados gerados conseguimos rastrear as chamadas internas que fazem parte da operação em si, como demonstra
a imagem abaixo:

![alt text](../images/open-tracing-002.png "OpenTracing")

No exemplo vemos que o  `trace-id 000001` foi gerado no `Serviço A` e propagado em todas as chamadas internas que 
a operação precisou fazer para atender a requisição do cliente.

Demais né?

Além de propagar os metadados os mesmos são enviados assíncronamente para uma ferramenta que os armazena e 
provendo funcionalidades, como por exemplo:

- Catálogo de serviços
    - Filtros por serviços
- Catálogo de operações
    - Filtros por metadados
    - Filtros por data
    - Filtros por duração
- Gráfico da operação

Com essas funcionalidades conseguimos visualizar quais serviços a operação passou e onde ocorreu o erro, como por 
exemplo na imagem abaixo:

![alt text](../images/open-tracing-003.png "OpenTracing")

Na imagem acima, conseguimos filtrar a operação de acordo com algum metadado e conseguimos visualizar os serviços que a 
operação precisou passar e quais são os tempos, etc.

O mercado e a comunidade conseguiram mitigar a complexidade de troubleshooting em sistemas distribuídos!

## Terminologia

Quando falamos sobre OpenTracing e sua especificação temos algumas terminologias e que são bastantes úteis para nós 
desenvolvedores:

### Span

Span é um período que representa uma operação, como por exemplo, uma requisição HTTP, na qual contém metadados extremamente 
importantes, como:

- Nome da operação
- Início da operação
- Término da operação
- Tags do span \ operação em si, como por exemplo: Nome do serviço, ip, método HTTP, etc.
- Baggages são pares de string para chave e valor que se aplicam ao Span, os quais se propagam em conjunto com o 
  próprio rastreamento, como por exemplo: identificador do usuário.
- Logs do span \ operação em si.

### Trace

Um trace é um conjunto de `span` contendo a ordem de execução dos mesmos, como por exemplo:

```text
––|–––––––|–––––––|–––––––|–––––––|–––––––|–––––––|–––––––|–> time

 [Span A··················································]
    [Span B···············································]
      [Span C·············································]
        [Span D···········································]
```

## Dicas

Utilize o `Baggage` para propagar informações de contexto do negócio, assim você consegue filtrar por eles e melhorar sua 
operação \ sustentação. Por exemplo, sempre propague o identificador do usuário, pois se algum usuário fizer uma reclamação
por conta de algum erro basta utilizar a ferramenta de OpenTracing para buscar por todas as operações com erro e 
que contenham o identificador do determinado usuário.

## Informações de suporte

Gostaria de saber mais sobre a especificação? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://opentracing.io/specification/)

Gostaria de saber mais sobre Tags? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_suporte/jaeger-concept-tags.md)

Gostaria de saber mais sobre Baggage? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_suporte/jaeger-concept-baggage.md)

Gostaria de saber mais sobre Logs? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_suporte/jaeger-concept-logs.md)
