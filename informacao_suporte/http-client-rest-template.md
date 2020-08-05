# Interagindo com sistemas externos usando RestTemplate

Uma das maneiras de se integrar com sistemas externos que expõe seus serviços
via HTTP é utilizando a classe [RestTemplate](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/client/RestTemplate.html) do Spring. A classe possui uma API fluida
que permite que possamos usar os principais métodos HTTP, como POST, GET, PUT entre outros.

Primeiro passado devemos identificar o método HTTP que devemos utilizar. Depois devemos indicar a URL
que o serviço se encontra e por fim invocar a configuração.

```java
RestTemplate restTemplate ...
String urlCartao = "http://localhost:8080/cartoes";
ResponseEntity<String> response = .......restTemplate.*;

```
Perceba que nosso retorno é tipado, ou seja podemos utilizar uma classe nossa que representa o retorno
da chamada HTTP, afinal nossa implementação consegue realizar a deserialização, porque nosso RestTemplate se
integra com frameworks como o Jackson por exemplo!!!

# Conhecendo o RestTemplate

Sempre quando aprendemos algo é super importante ir mais fundo, e quando falamos de RestTemplate, por exemplo, existem 
várias configurações que podem atender seu cenário!

Vamos aprender mais sobre [@RestTemplate](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/client/RestTemplate.html)?

O RestTemplate é um HTTP Client que possibilita você fazer chamadas HTTP, logo podemos utilizar todos os verbos HTTP, 
como por exemplo:

Verbo GET

```java
// Método
restTemplate.getForObject(url, resposta);

// Exemplo
restTemplate.getForObject("http://localhost:8080/v1/propostas/5951feee-9901-4111-83af-38cbe2895ffc, GetProposta.class);
```

Verbo POST

```java
// Método
restTemplate.postForObject(url, body, resposta);

// Exemplo
restTemplate.postForObject("http://localhost:8080/v1/propostas, novaProposta, PostProposta.class);
```

Verbo PUT

```java
// Método
restTemplate.putForObject(url, body, resposta);

// Exemplo
restTemplate.putForObject("http://localhost:8080/v1/propostas/5951feee-9901-4111-83af-38cbe2895ffc, atualizarProposta, PostProposta.class);
```

Verbo PATCH

```java
// Método
restTemplate.patchForObject(url, body, resposta);

// Exemplo
restTemplate.patchForObject("http://localhost:8080/v1/propostas/5951feee-9901-4111-83af-38cbe2895ffc, atualizarProposta, PostProposta.class);
```

Verbo DELETE

```java
// Método
restTemplate.delete(url);

// Exemplo
restTemplate.delete("http://localhost:8080/v1/propostas/5951feee-9901-4111-83af-38cbe2895ffc");
```

Demais né! Talvez esteja pensando e quando ocorrer erro na faixa do 4xx e 5xx, como lidar?

Quando ocorre erro na faixa do 4xx ou 5xx o RestTemplate lança uma exceção específica para cada família de status do HTTP, 
como por exemplo:

- [HttpClientErrorException](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/client/HttpClientErrorException.html): Em caso de erro 4xx
- [HttpServerErrorException](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/client/HttpServerErrorException.html): Em caso de erro 5xx

Se não deseja segmentar por faixa de status code, não tem problema, basta tratar a exceção [HttpStatusCodeException](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/client/HttpStatusCodeException.html).

Pronto! Agora sabemos lidar com erro!

Se quiser obter a resposta do erro, como por exemplo o body, existe um método para isto o [getResponseBodyAsString](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/client/RestClientResponseException.html#getResponseBodyAsString--);

Pronto! Estamos mais preparados para lidar com os cenários da Zup!

# Informações de Suporte

- Tem dúvida de como o Jackson funciona? [Este link entra em detalhes de como podemos usar essa biblioteca
para nos ajudar a trabalhar com json](https://github.com/FasterXML/jackson-databind)


