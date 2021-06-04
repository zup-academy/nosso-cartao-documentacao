# Como expor uma API GET no Spring?

Para expor uma API GET no Spring devemos utilizar a anotação [@GetMapping](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/GetMapping.html).

1º Precisamos criar um Controller com a anotação [@RestController](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/bind/annotation/RestController.html).

```java
@RestController
public class MeuController {
   // código omitido
}
```

2º Precisamos criar nossa API de acordo com o objetivo e seu método HTTP.

```java
@RestController
public class MeuController {

    @GetMapping("/v1/minha-api")
    public ResponseEntity<?> minhaOperacao() {
        // código omitido
        return ResponseEntity.status(status).body(body);
    }

}
```

Pronto!

Agora já sabemos como usar a anotação @GetMapping!

# Como receber dados na minha API GET utilizando Spring?

Existem duas formas de receber dados em uma requisição HTTP do tipo GET, como por exemplo:

- Via Path Parameter, como por exemplo `https://localhost:8080/proposta/0e5d2c91-f987-4f84-ba85-d0a5edb48225` o 
identificador do recurso é passado no Path Parameter `0e5d2c91-f987-4f84-ba85-d0a5edb48225`

- Via Query Parameter, como por exemplo `https://localhost:8080/proposta?status=ATIVO` o filtro por status `ATIVO` é 
passado no Query Parameter

Vamos fazer isso utilizando Spring?

Primeiro vamos começar recebendo Path Parameter e para isso o Spring provê uma anotação bem intuitiva denominada 
[@PathVariable](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/bind/annotation/PathVariable.html)
, conforme exemplo abaixo:

```java
@RestController
public class MeuController {

    @GetMapping("/v1/propostas/{identificador}")
    public ResponseEntity<?> obterProposta(@PathVariable("identificador") String identificador) {
        // código omitido
        return ResponseEntity.status(status).body(body);
    }

}
```

Para mapear o Path Parameter no Spring, você tem que passar a expressão `{NOME_DA_VARIÁVEL}` na sua API, conforme 
exemplo abaixo:

```java
@GetMapping("/v1/propostas/{identificador}")
```

Para receber o Path Parameter no Spring, você tem que utilizar o nome da expressão mapeada na anotação @PathVariable, 
conforme exemplo abaixo!

```java
@GetMapping("/v1/propostas/{identificador}")
public void ...(@PathVariable("identificador") String identificador)
```

Demais né! Vamos complementar recebendo Query Parameter?

Para mapear e receber Query Parameter o Spring provê uma anotação bem intuitiva denominada [@RequestParam](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/bind/annotation/RequestParam.html)
, conforme exemplo abaixo:

```java
@RestController
public class MeuController {

    @GetMapping("/v1/propostas")
    public ResponseEntity<?> obterProposta(@RequestParam(name = "status", required = false, defaultValue = "ATIVO") String status) {
        // código omitido
        return ResponseEntity.status(status).body(body);
    }

}
```

Neste nosso exemplo a gente mapeou em nossa API o query parameter `status` como sendo opcional, caso não passado o valor 
padrão será `ATIVO`, demais né!

Pronto!

Agora já sabemos como usar a anotação @GetMapping, @PathVariable e @RequestParam!

## Informação de Suporte

Quer saber mais sobre como criar API's REST no Spring? [Aqui você encontra como fazer isso!](https://spring.io/guides/gs/rest-service/)
