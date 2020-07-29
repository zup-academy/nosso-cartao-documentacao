# Qual objetivo do método PATCH do REST \ HTTP?

O método PATCH é utilizado para atualização parcial de um determinado recurso, como por exemplo?

```
PATCH http://localhost:8080/v1/carros/cc0cfe13-edce-4fe4-a12d-90b32bb844ba

{
   "nome" : "Gol"
}
```

Olhando o método e o recurso sabemos que estamos atualizando somente o nome do carro com o identificador 
`cc0cfe13-edce-4fe4-a12d-90b32bb844ba`, os outros atributos não são alterados.