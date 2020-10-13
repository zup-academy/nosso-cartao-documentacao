# Como usar o UriComponentsBuilder ???

É uma classe utilitária do Spring que nos ajuda a criar URIs. Essa classe nos ajuda a lidar
com problemas comuns de encodings presentes nas URIs.

## Usando UriComponentsBuilder no seu RestController

Uma característica bastante interessante no Spring é que o objeto UriComponentsBuilder é injetado automaticamente nos metodos
de um método no Controller. Veja um exemplo abaixo:

```java
@PostMapping
public ResponseEntity<PropostaCriada> novaProposta(@RequestBody @Valid NovaProposta novaProposta, UriComponentsBuilder uriComponentsBuilder) {
    // Código omitido
}
```

Perceba que não foi utilizada nenhuma anotação declarativamente no método do controller, 
mas o Spring consegue injetar automaticamente o objeto com sucesso. Primeiro passo concluído
com sucesso, agora precisamos retornar o **Response** configurado corretamente com o Header **Location**.

Veja um exemplo prático de como fazer isso:

```java
@PostMapping
public ResponseEntity<PropostaCriada> novaProposta(@RequestBody @Valid NovaProposta novaProposta, UriComponentsBuilder uriComponentsBuilder) {
  // Código omitido
  return ResponseEntity.created(uriComponentsBuilder.path("/propostas/{id}").buildAndExpand(nova.getId()).toUri()).body(nova);
}
``` 

Um ponto bastante interessante é que o próprio _UriComponentsBuilder_ consegue gerenciar o endereço
do servidor baseado nas próprias configurações internas da aplicação.

Pronto!!! 

Agora já sabemos como usar a classe _UriComponentsBuilder_ de acordo com as práticas recomendadas pelo
Spring. 
