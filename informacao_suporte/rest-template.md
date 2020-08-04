# Interagindo com sistemas externos usando RestTemplate

Uma das maneiras de se integrar com sistemas externos que expõe seus serviços
via HTTP é utilizando a classe [RestTemplate](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/client/RestTemplate.html) do Spring. A classe possui uma API fluída
que permite que possamos usar os principais métodos HTTP, como POST, GET, PUT entre outros.

Primeiro passado devemos identificar o método HTTP que devemos utilizar. Depois devemos indicar a URL
que o serviço se encontra e por fim invocar a configuração.

```java
RestTemplate restTemplate ...
String urlCartao = "http://localhost:8080/cartoes";
ResponseEntity<String> response = .......restTemplate.*;

```
Perceba que nosso retorno é tipado, ou seja podemos utilizar uma classe nossa que represente o retorno
da chamada HTTP, afinal nossa implementação consegue realizar a deserialização, porque nosso RestTemplate se
integra com frameworks como o Jackson por exemplo!!!

# Informações de Suporte

- Tem dúvida de como o Jackson funciona??? [Este link entra em detalhes de como podemos usar essa biblioteca
para nos ajudar a trabalhar com json](https://www.baeldung.com/jackson-object-mapper-tutorial)


