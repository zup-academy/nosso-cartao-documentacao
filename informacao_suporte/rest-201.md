# Mas porque 201? Entendendo um pouco sobre REST!!!

Seguindo o estilo arquitetural REST temos que aplicar algumas características que o modelo define.

Toda criação de um novo recurso deve ser realizada utilizando o método **HTTP POST** e quando essa operação
for realizada com sucesso ele deve retornar o status code **201** indicando que o recurso foi criado com sucesso.

Adicionalmente você pode incluir o elemento criado no _Body_ na resposta da requisição caso você precise. Outra prática
recomendada é incluir o cabeçalho **Location** na sua resposta. Se você tem dúvida como fazer isso
usando o Spring [veja neste material !!!](../informacao_suporte/spring-response-entity.md)

## Vamos fazer isso com Spring, então!!!

```java
  @PostMapping
  public ResponseEntity<PropostaCriada> novaProposta(@RequestBody @Valid NovaProposta novaProposta,
      UriComponentsBuilder uriComponentsBuilder){
    var nova = this.criacaoDaProposta.nova(novaProposta);
    return ResponseEntity.created(uriComponentsBuilder.buildAndExpand("/propostas/{id}",nova).toUri()).body(nova);
  }
```
**@PostMapping** aqui nosso código faz a relação com o verbo HTTP POST. Perceba que no retorno do nosso
método chamamos a classe **ResponseEntity.created()** com isso seguimos nossa prática
recomendada, para criação verbo **HTTP POST** e retorno com status **201**.


#Informação de Suporte

Quer conhecer mais sobre REST e ver todos os status codes e suas descrições [Veja Aqui !!!](../informacao_suporte/rest-status.md)

Procura uma descrição mais detalhada do que essa prática recomenda. [Neste link você pode encontrar](https://restfulapi.net/http-status-201-created/) 