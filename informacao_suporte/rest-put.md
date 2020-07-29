# Qual objetivo do método PUT do REST \ HTTP?

O método PUT é utilizado para atualização completa de um determinado recurso, como por exemplo?

```
PUT http://localhost:8080/v1/carros/cc0cfe13-edce-4fe4-a12d-90b32bb844ba

{
   "nome" : "Gol",
   "ano" : 2019
}
```

Olhando o método e o recurso sabemos que estamos atualizando todos os atributos do carro com o identificador 
`cc0cfe13-edce-4fe4-a12d-90b32bb844ba`.

De acordo com a [especificação](https://tools.ietf.org/html/rfc7231#section-4.3.4) do REST, caso o recurso não for encontrado deve-se criar um, ou seja, caso o carro com o
identificador `cc0cfe13-edce-4fe4-a12d-90b32bb844ba` não existir, devemos criar um novo.

Porém essa pratica não é muito aplicada pelo mercado, pois utiliza-se o método POST para tal objetivo.

#Informação de Suporte

Como expor uma API PUT no Spring? [Aqui você encontra como fazer isso !!!](../informacao_suporte/spring-put-api.md)

Quer saber mais sobre a especificação, acesse o [link!](https://tools.ietf.org/html/rfc7231#section-4.3.4)