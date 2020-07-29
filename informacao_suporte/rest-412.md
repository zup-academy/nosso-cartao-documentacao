# Mas porque 412? Entendendo um pouco sobre REST!!!

Seguindo o estilo arquitetural REST temos que aplicar algumas características que o modelo define, portanto, todo erro 
de entrada devemos representar como **412 Precondition Failed**, pois algumas das informações obrigatórias foi ou 
foram violada(s).

Geralmente nos projetos são definidos um padrão de erro para melhorar a identificação do mesmo, conforme exemplo abaixo:

```json
POST http://localhost:8080/v1/cars

HTTP/1.1 412 Precondition Failed
Content-Type: application/json
{
  "messages": [
    {
      "code": "412.003",
      "description": "Missing or invalid name field."
    },
    {
      "code": "412.004",
      "description": "Missing or invalid address field."
    },
    {
      "code": "412.001",
      "description": "Missing or invalid document field."
    }
  ]
}
```
## Vamos fazer isso com Spring, então!!!

O Spring provê uma classe denominada ResponseEntity na qual você consegue passar todas as informações da requisição HTTP, 
como por exemplo, status, body, header, etc.

```java
public ResponseEntity<?> novaProposta(){
    ....
    return ResponseEntity.status(HttpStatus.PRECONDITION_FAILED).body(body);
}
```

# Informação de Suporte

Quer saber mais sobre status code, acesse o [link!](../informacao_suporte/rest-status.md)

Quer saber mais sobre REST, acesse o [link!](https://restfulapi.net/)