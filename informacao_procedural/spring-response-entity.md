# Como modelar nosso HTTP Response com Spring

Quando escolhemos seguir o modelo arquitetural REST devemos seguir as práticas sugeridas pelo modelo,
nesse caso o modelo define um modelo rigoroso no controle de Status Code na resposta. Se você tem dúvida pode clicar
aqui.

Então precisamos de um modelo que nos ajude mapear essas práticas com nossos Controllers que foram implementados
com Spring.
O framework possui a classe [ResponseEntity](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/http/ResponseEntity.html) que é uma abstração completa para o Response, nela temos como definir
os Headers, Body e Status Code de uma resposta HTTP, e é essa classe que vamos explorar agora!!!

## Modelando status code

Para os status code mais comum a classe nos fornece métodos estáticos que permitem que criemos
instâncias de uma maneira mais declarativa, usando uma api mas fluída, vamos ver alguns exemplos
```java

// Status Code 200
ResponseEntity.ok()

// Status Code 202
ResponseEntity.accepted()

// Status Code 204
ResponseEntity.noContent()

// Status Code 400
ResponseEntity.badRequest()

// Status Code 404
ResponseEntity.notFound()

```
Como podemos ver esses métodos são bastante declarativos como podemos ver, mas ainda temos que lidar
com o Body da requisição como podemos fazer isso??  _exceto quando utilizamos o Status Code 204_

## Manipulando o Body da requisição

Sabemos como modelar o Status code e agora como podemos manipular o Body da requisição HTTP, a classe [ResponseEntity](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/http/ResponseEntity.html)
possui métodos que também nos auxiliam, vamos dar uma olhada neles

### Usando métodos pré-definidos
Podemos combinar a definição de Status Code mais definição do Body, criando uma maneira mais fluída de código

```java
ResponseEntity.ok().body("Body")
```
Nesse caso nossa operação retornou código 200, operação efetuada com sucesso e retornou o conteúdo **Body**.
Veja como o método _body()_ é utilizado permitindo a definição do conteúdo do corpo da nossa resposta.



### Customizando Status Code 
Em algumas situações precisamos usar um Status Code que não possui um método pré-definido, nesse
caso pode usar o método _status()_ combinado com a nossa denição de body usando novamente o
método _body()_. Vamos ver essa construção

```java
ResponseEntity.status(HttpStatus.CONFLICT).body("Elemento ja criado");
```
Como podemos ver usamos o Status Code de conflito **409**, e logo depois fizemos a definição do
body.


## Configurando Headers

