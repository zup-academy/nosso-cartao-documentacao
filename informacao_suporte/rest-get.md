# Qual objetivo do método GET do REST \ HTTP?

O método GET é utilizado para recuperação de um determinado recurso, como por exemplo?

```
GET http://localhost:80808/v1/carros/cc0cfe13-edce-4fe4-a12d-90b32bb844ba
```

Olhando o método e o recurso sabemos que estamos buscando o carro com identificador `cc0cfe13-edce-4fe4-a12d-90b32bb844ba`.

Quando não há identificador, sabemos que estamos buscando todos os recursos, ou seja, todos os carros.

```
GET http://localhost:80808/v1/carros
```