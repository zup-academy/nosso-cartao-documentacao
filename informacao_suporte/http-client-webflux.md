# Spring WebClient uma API mais fluída para realizar requisições

Com o lançamento da versão 5 do framework, foi criada uma nova maneira de realizar
chamadas para sistemas externos que exponham seus serviços via HTTP.

Essa nova API suporta chamadas assíncronas ou síncronas, então caso você opte
por usar uma versão do Spring que dê suporte ao WebFlux você pode usá-la. 

Assim como o RestTemplate o Spring Webclient delega a conexão e transporte para uma biblioteca HTTP.  

## Versão Síncrona

```java

WebClient client = WebClient.create();
Cartao cartao = client.get().uri("http://localhost:9999/api/cartoes/1111").retrieve().bodyToMono(Cartao.class).block()

```

Vamos explorar um pouco a construção acima. Utilizamos o verbo _HTTP GET_, logo em seguida indicamos qual _URI_ nosso serviço está disponível,
fazemos algumas conversões e serializações e por fim explicitamente a instrução **block()** que torna nossa versão 100% síncrona.

Como podemos perceber essa API é mais recente e tem um design um pouco mais fluído e permite
com que consigamos identificar as características de uma chamada HTTP nas próprias chamadas de métodos.

## Versão Assíncrona

Quando utilizamos a versão reativa do Spring, devemos utilizar a versão do
WebClient que é capaz de lidar com todas características reativas.

Um detalhe bastante importante é que durante a construção do código não há mudanças
significativas, porém na execução mudamos nosso modo de pensar e utilizamos um modelo
de programação funcional.

```java
 
WebClient client = WebClient.create();
Mono<Cartao> cartao = client.get().uri("http://localhost:9999/api/cartoes/1111").retrieve().bodyToMono(Cartao.class)

```

## Informações de Suporte

- O que é Spring [Webflux](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html)?
- Quer descobrir que biblioteca o Spring WebClient usa por padrão. [Clique aqui!](https://github.com/reactor/reactor-netty)
- Ainda tenho algumas dúvidas sobre o WebClient. [A documentação completa você pode encontrar aqui.](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html#webflux-client)
- Se você está curioso e quer ver como podemos implementar uma pequena aplicação utilizando a stack reativa do
spring. [Este link é um guia inicial para investir nessa jornada](https://spring.io/guides/gs/reactive-rest-service/)

- Você pode encontrar a documentação completa de toda a stack reativa neste [link](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html#spring-webflux)
