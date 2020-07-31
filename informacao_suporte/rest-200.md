# Mas porque 200? Entendendo um pouco sobre REST!!!

Seguindo o estilo arquitetural REST temos que aplicar algumas características que o modelo define.

Toda operação realizada com sucesso ela deve retornar o status code **200**, porém temos algumas regras a serem seguidas:

- Os métodos GET, PUT, PATCH e DELETE são operações de alteração ou obtenção de um determinado recurso, portanto devemos
retornar 200.

- Quando utilizado o método POST para criação de um determinado recurso devemos retornar [201](rest-201.md).

- Quando utilizado o método POST para ordenar algo, como por exemplo: Enviar email, resetar senha, etc. Devemos retornar 200.

## Vamos fazer isso com Spring, então!!!

O Spring provê uma classe denominada ResponseEntity na qual você consegue passar todas as informações da requisição HTTP, 
como por exemplo, status, body, header, etc.

```java
public ResponseEntity<?> obterProposta(){
    // Código omitido
    return ResponseEntity.status(HttpStatus.OK).body(body);
}
```

# Informação de Suporte

Quer saber mais sobre status code? Acesse o [link!](../informacao_suporte/rest-status.md)

Quer saber mais sobre REST? Acesse o [link!](https://restfulapi.net/)

Quer saber sobre a especificação? Acesse o [link!](https://tools.ietf.org/html/rfc7231#section-6.3.1)