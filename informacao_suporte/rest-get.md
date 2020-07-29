# Qual objetivo do método GET do REST \ HTTP?

O método GET é utilizado para **obter** um ou vários recursos, como por exemplo?

```
GET http://localhost:8080/v1/carros/cc0cfe13-edce-4fe4-a12d-90b32bb844ba
```

Olhando o método e o recurso sabemos que estamos buscando o carro com identificador `cc0cfe13-edce-4fe4-a12d-90b32bb844ba`.

Um outro exemplo é quando não tem um identificador do recurso:

```
GET http://localhost:8080/v1/carros
```

Quando não há identificador, sabemos que estamos buscando todos os recursos, ou seja, todos os carros.

#Informação de Suporte

Como expor uma API GET no Spring? [Aqui você encontra como fazer isso !!!](../informacao_suporte/spring-get-api.md)

Quer saber mais sobre a especificação, acesse o [link!](https://tools.ietf.org/html/rfc7231#section-4.3.1)