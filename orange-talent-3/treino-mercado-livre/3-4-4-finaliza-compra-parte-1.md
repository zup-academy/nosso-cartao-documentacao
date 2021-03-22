# Realmente finaliza compra - parte 1

### Contexto

Aqui a gente vai simular uma integração com um gateway como paypal, pagseguro etc. O fluxo geralmente é o seguinte:

*   O sistema registra uma nova compra e gera um identificador de compra que pode ser passado como argumento para o gateway.
*   O cliente efetua o pagamento no gateway
*   O gateway invoca uma url do sistema passando o identificador de compra do próprio sistema e as informações relativas a transação em si.

Então essa é a parte 1 do processo de finalização de compra. Onde apenas geramos a compra no sistema. Não precisamos da noção de um carrinho compra. Apenas temos o usuário logado comprando um produto.

### Necessidades

*   A pessoa pode escolher a quantidade de itens daquele produto que ela quer comprar
*   O estoque do produto é abatido 
*   Um email é enviado para a pessoa que é dona(o) do produto informando que um usuário realmente disse que queria comprar seu produto.
*   Uma compra é gerada informando o status INICIADA e com as seguintes informações:
*   gateway escolhido para pagamento
*   produto escolhido
*   quantidade
*   comprador(a)
*   Suponha que o cliente pode escolher entre pagar com o Paypal ou Pagseguro.

### Restrições

*   A quantidade é obrigatória
*   A quantidade é positiva
*   Precisa ter estoque para realizar a compra​

### **Resultado esperado**

*   Caso a pessoa escolha o paypal seu endpoint deve gerar o seguinte redirect(302):
    *   Retorne o endereço da seguinte maneira: paypal.com/{idGeradoDaCompra}?redirectUrl={urlRetornoAppPosPagamento}
*   Caso a pessoa escolha o pagseguro o seu endpoint deve gerar o seguinte redirect(302):
    *   Retorne o endereço da seguinte maneira: pagseguro.com?returnId={idGeradoDaCompra}&redirectUrl={urlRetornoAppPosPagamento}
*   Caso aconteça alguma restrição retorne um status 400 informando os problemas. 

### Você está no filé do código

Aqui é para ser muito recompensador! Você já se esforçou demais, fez muita feature, deve ter gostado de algumas dicas, se questionado em relação as outras, não concordado com outras tantas. Só que, acima de tudo, você ESTUDOU E TREINOU. Tente implementar a feature completamente sozinho(a). Invista o tempo necessário, o tempo aqui é seu amigo e não seu inimigo. O foco é seu desenvolvimento!

### Antes de começar
Por favor descreva como você pretende realizar a implementação deste desafio. Para acessar o formulário [clique aqui](https://forms.gle/NerMmk1PkaTiZXNz9)

### **informações de suporte geral**

1.  Lembre que uma das coisas mais importante do pilar "a prioridade é funcionar" é que você deve maximizar a execução do seu código. Planeje o que você quer fazer e implemente passo a passo. Faça uma pequena parte e execute. 
2.  Quais restrições você pode colocar na compra para garantir que ela nunca seja criada em um estado inválido?
3.  Qual tática você vai utilizar que vai enviar o email?
4.  Como você vai representar o gateway?
5.  Como você vai verificar o estoque? Vai ter um método de consulta e outro que altera o objeto? E se entre a consulta e o abate algum outro pedido de compra no sistema? 
6.  Será que você fez um if para decidir qual endereço vai ser retornado para o redirect? Será que precisamos desse if?
7.  O que merece ser testado? Já falamos um pouco sobre isso e os prós e contras. Eu continuo entendendo que a prioridade são fluxos de código que possuem branches(ifs, eles, loops etc). [Falo mais aqui](https://youtu.be/vCnhwbkX3EA).
9.  [Como Alberto faria esse código](https://youtu.be/HP9OhAvwOu0) Lembrando que aqui é a parte inicial. Ainda falta a volta :). 
10. Como Alberto faria os testes? Você encontra em duas partes: [PARTE 1](https://youtu.be/CnDoQahMoD0) e [PARTE 2](https://youtu.be/t8sJeUS3nz4). 


### informações de suporte para a combinação Java/Kotlin + Spring​

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/H6aM-4RaRrE)
5.  [Como externalizar as mensagens de erro no arquivo de configuração.](https://youtu.be/FO4HnZNCvoo)
6.  Use e abuse das annotations da bean validation para indicar as restrições dos parâmetros. 
7.  Brinque um pouco com a classe **_Assert_**​ ​do Spring para fazer checagens de parâmetro também. As ideias de Design By Contract ajudam demais a aumentar a confiabilidade da aplicação.
8.  Para configurar o Spring Security olhe [aqui](https://youtu.be/0I--CLsqC7w)
9.  Lembrando que, para receber a referência para o usuário logado no método do controller, você pode usar a annotation _@AuthenticationPrincipal_​.

### Depois de finalizar
Antes de passar para a próxima funcionalidade, envie o link para o diff da sua solução acessando [este formulário](https://forms.gle/MXRUCzr3c6EGxkdp6)

