# Mas porque 404? Entendendo um pouco sobre REST!!!

Seguindo o estilo arquitetural REST temos que aplicar algumas características que o modelo define, portanto, todo recurso
não encontrado devemos representar como **404 Not Found**.

Geralmente nos projetos são definidos um padrão de erro para melhorar a identificação do mesmo, conforme exemplo abaixo:

```json
POST http://localhost:8080/v1/propostas

HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "messages": [
    {
      "code": "404.001",
      "description": "Proposta não encontrada."
    }
  ]
}
```

## Vamos fazer isso com Spring, então!!!

O Spring provê uma classe denominada ResponseEntity na qual você consegue passar todas as informações da requisição HTTP, 
como por exemplo, status, body, header, etc.

```java
public ResponseEntity<?> obterProposta(){
    // Código omitido
    return ResponseEntity.status(HttpStatus.NOT_FOUND).body(body);
}
```

# Informação de Suporte

Quer saber mais sobre status code? Acesse o [link!](../informacao_suporte/rest-status.md)

Quer saber mais sobre REST? Acesse o [link!](https://restfulapi.net/)

Quer saber sobre a especificação? Acesse o [link!](https://tools.ietf.org/html/rfc7231#section-6.5.4)