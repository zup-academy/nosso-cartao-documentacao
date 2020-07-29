# Mas porque 422? Entendendo um pouco sobre REST!!!

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

## Quer saber mais sobre status code, acesse o [link!](https://restfulapi.net/http-status-codes/)