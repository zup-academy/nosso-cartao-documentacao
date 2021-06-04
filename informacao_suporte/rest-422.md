# Mas porque 422? Entendendo um pouco sobre REST!

Seguindo o estilo arquitetural REST temos que aplicar algumas características que o modelo define, portanto, todo erro 
de negócio devemos representar como **422 Unprocessable Entity**, pois as informações obrigatórias foram preenchidas 
porém alguma regra de negócio foi violada.

Geralmente nos projetos são definidos um padrão de erro para melhorar a identificação do mesmo, conforme exemplo abaixo:

```json
POST http://localhost:8080/v1/cars

HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json

{
  "messages": [
    {
      "code": "422.001",
      "description": "Document already exists."
    }
  ]
}
```

## Vamos fazer isso com Spring!

O Spring provê uma classe denominada ResponseEntity na qual você consegue passar todas as informações da requisição HTTP, 
como por exemplo, status, body, header, etc.

```java
public ResponseEntity<?> novaProposta(){
    // Código omitido
    return ResponseEntity.status(HttpStatus.UNPROCESSABLE_ENTITY).body(body);
}
```

## Informação de Suporte

Quer saber mais sobre status code? Acesse o [link!](../informacao_suporte/rest-status.md)

Quer saber mais sobre REST? Acesse o [link!](https://restfulapi.net/)

Quer saber sobre a especificação? Acesse o [link!](https://tools.ietf.org/html/rfc4918#section-11.2)
