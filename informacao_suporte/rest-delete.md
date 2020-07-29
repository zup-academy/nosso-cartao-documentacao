# Qual objetivo do método DELETE do REST \ HTTP?

O método DELETE é utilizado para remover um ou vários recursos, como por exemplo?

```
DELETE http://localhost:8080/v1/carros/cc0cfe13-edce-4fe4-a12d-90b32bb844ba
```

Olhando o método e o recurso sabemos que estamos removendo o carro com identificador `cc0cfe13-edce-4fe4-a12d-90b32bb844ba`.

Um outro exemplo é quando não tem um identificador do recurso:

```
DELETE http://localhost:8080/v1/carros
```

Quando não há identificador, sabemos que estamos removendo todos os recursos, ou seja, todos os carros.

Cuidado com essa última abordagem, pois você está removendo todos os recursos do seu sistema!