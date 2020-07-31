# Mas porque 201? Entendendo um pouco sobre REST!!!

Seguindo o estilo arquitetural REST temos que aplicar algumas características que o modelo define.

Toda criação de um novo recurso deve ser realizada utilizando o método **HTTP POST** e quando essa operação
for realizada com sucesso ele deve retornar o status code **201** indicando que o recurso foi criado com sucesso.

Adicionalmente você pode incluir o elemento criado no _Body_ na resposta da requisição caso você precise. Outra prática
recomendada é incluir o cabeçalho **Location** na sua resposta. Se você tem dúvida como fazer isso
usando o Spring [veja neste material !!!](../informacao_suporte/spring-response-entity.md)

## Vamos fazer isso com Spring, então!!!

O Spring provê uma classe denominada ResponseEntity na qual você consegue passar todas as informações da requisição HTTP, 
como por exemplo, status, body, header, etc.

```java
@PostMapping
public ResponseEntity<?> novaProposta(@RequestBody @Valid ....){
    // Código omitido
    return ResponseEntity.created(uriComponentsBuilder.buildAndExpand("/resource/{id}", id).toUri()).body(body);
}
```

**@PostMapping** aqui nosso código faz a relação com o verbo HTTP POST. Perceba que no retorno do nosso
método chamamos a classe **ResponseEntity.created()** com isso seguimos nossa prática
recomendada, para criação verbo **HTTP POST** e retorno com status **201**.

# Informação de Suporte

Quer saber mais sobre status code? Acesse o [link!](../informacao_suporte/rest-status.md)

Quer saber mais sobre REST? Acesse o [link!](https://restfulapi.net/)

Quer saber sobre a especificação? Acesse o [link!](https://tools.ietf.org/html/rfc7231#section-6.3.2)