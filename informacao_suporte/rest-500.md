# Mas porque 500? Entendendo um pouco sobre REST!

Seguindo o estilo arquitetural REST temos que aplicar algumas características que o modelo define, portanto, todo erro 
não tratado, devemos representar como **500 Internal Server Error**, pois indica que o servidor encontrou um erro 
inesperado.

## Vamos fazer isso com Spring!

O Spring provê uma classe denominada ResponseEntity na qual você consegue passar todas as informações da requisição HTTP, 
como por exemplo, status, body, header, etc.

```java
public ResponseEntity<?> novaProposta(){
    // Código omitido
    return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(body);
}
```

## Informação de Suporte

Quer saber mais sobre status code? Acesse o [link!](../informacao_suporte/rest-status.md)

Quer saber mais sobre REST? Acesse o [link!](https://restfulapi.net/)

Quer saber sobre a especificação? Acesse o [link!](https://tools.ietf.org/html/rfc7231#section-6.6.1)
