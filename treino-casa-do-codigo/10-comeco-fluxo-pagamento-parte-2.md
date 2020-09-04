# Começo do fluxo de pagamento parte 2

## necessidades

Vamos receber também o parâmetro relativo ao carrinho de compras na requisição relativa aos dados da pessoa que está comprando. O json montado pelo cliente relativo ao carrinho tem o seguinte schema:

```
{
  "total": decimal,
  "itens":[
     {
      "idLivro":number,
      "quantidade": "number"
    },
     {
      "idLivro":number,
      "quantidade": "number"
    }
  ]
}
```

Reforçando aqui a explicação. A nossa aplicação da casa do código é divida em dois projetos. Temos a aplicação cliente e a aplicação que roda no backend. Neste cenário, toda lógica de construção do carrinho de compras ficou na aplicação cliente e, por conta disso, ela precisa enviar essa informação para o endpoint na mesma requisição que pegamos os dados da pessoa que estiver comprando. 


### restrição

* o total é não nulo
* o total é maior que zero
* tem pelo menos um item no carrinho
* idLivro é obrigatório
* idLivro precisa existir no banco de dados
* quantidade é obrigatória
* quantidade é maior que zero
* o total calculado no servidor precisa ser igual ao total enviado

### resultado esperado

* Em caso de tudo estar correto, uma nova compra deve ser gerada com todos os dados da pessoa que está comprando e também com as informações relativas ao carrinho de compras. No fim, retorne o status 201 com um endereço apontando onde os detalhes da compra podem ser encontrados.
* Em caso de falha de validação retorne 400