# Realmente finaliza a compra - parte 2

### Contexto

Aqui estamos lidando com o retorno do gateway de pagamento

### Necessidades

O meio de pagamento(pagseguro ou paypal) redireciona para a aplicação passando no mínimo 3 argumentos:

*   id da compra no sistema de origem
*   id do pagamento na plataforma escolhida
*   status da compra. Para o status vamos assumir os dois básicos(Sucesso, Falha). Os gateways de pagamento informam isso de maneira distinta.
*   Paypal retorna o número 1 para sucesso e o número 0 para erro.
*   Pagseguro retorna a string SUCESSO ou ERRO.

Temos alguns passos aqui.

*   Precisamos registrar a tentativa de pagamento com todas as informações envolvidas. Além das citadas, é necessário registrar o exato instante do processamento do retorno do pagamento.
*   Caso a compra tenha sido concluída com sucesso:
    *   precisamos nos comunicar com o setor de nota fiscal que é um outro sistema. Ele precisa receber apenas receber o id da compra e o id do usuário que fez a compra.
    *   Neste momento você não precisa criar outro projeto para simular isso. Crie um controller com um endpoint fake e faça uma chamada local mesmo.
    *   também precisamos nos comunicar com o sistema de ranking dos vendedores. Esse sistema recebe o id da compra e o id do vendedor.
    *   Neste momento você não precisa criar outro projeto para simular isso. Faça uma chamada local mesmo.
*   para fechar precisamos mandar um email para quem comprou avisando da conclusão com sucesso. Pode colocar o máximo de informações da compra que puder.
*   Caso a compra não tenha sido concluída com sucesso, precisamos:
    *   enviar um email para o usuário informando que o pagamento falhou com o link para que a pessoa possa tentar de novo.

### Restrição

*   id de compra, id de transação e status são obrigatórios para todas urls de retorno de dentro da aplicação.
*   O id de uma transação que vem de alguma plataforma de pagamento só pode ser processado com sucesso uma vez.
*   Uma transação que foi concluída com sucesso não pode ter seu status alterado para qualquer coisa outra coisa.
*   Uma compra não pode ter mais de duas transações concluídas com sucesso associada a ela.

### Antes de começar
Por favor descreva como você pretende realizar a implementação deste desafio. Para acessar o formulário [clique aqui](https://forms.gle/cmNZnUGtrfFAGnhu7)

### Desafio extra 1

*   O email não precisa ser real, manda um ```System.out.println```. Mas o sistema precisa estar preparado para enviar email real em produção.

### Desafio extra 2

*   Temos duas plataformas de pagamento externas neste momento, vamos ter mais, como seu código ficaria preparado para esse requisito de negócio?


### Resultado esperado

*   Status 200 dizendo retornando o status do pagamento.
*   Em caso de erro de validação, retorne 400 e o json com erros.

### Você está no super filé do código

Passou pela primeira parte do fechamento da compra? Agora é ainda mais desafiador. Você vai precisar juntar tudo que trabalhamos. E ainda tem uma coisa especial que é uma necessidade mais forte de generalização. Eu espero que você aproveite e fique ainda mais preparado(a) para enfrentar os próximos desafios. 

### Informações de suporte geral

1.  Lembre que uma das coisas mais importante do pilar "a prioridade é funcionar" é que você deve maximizar a execução do seu código. Planeje o que você quer fazer e implemente passo a passo. Faça uma pequena parte e execute. 
2.  Quais restrições você pode colocar na compra para garantir que ela nunca tenha tentativas de pagamentos num estado inválido associado a ela? 
3.  Você tem um desafio grande de divisão de responsabilidade aqui. São muitas coisas que precisam ser feitas. Como que você vai usar uma estratégia de design de código para manter esse código entendível?
4.  Como você vai associar tentativas de pagamento que vem de gateways diferentes?
5.  Será que você usou if para gerar as tentativas de pagamento de gateways diferentes?
6.  O que merece ser testado? Já falamos um pouco sobre isso e os prós e contras. Eu continuo entendendo que a prioridade são fluxos de código que possuem branches(ifs, eles, loops etc). [Falo mais aqui](https://youtu.be/vCnhwbkX3EA). 
9.  Como Alberto faria esse código? [Parte 1](https://youtu.be/b5vUoPygtv4), [parte 2](https://youtu.be/_QYVYx2ENDQ), [parte 3](https://youtu.be/AAugW3C54Cs)
10. Como Alberto testaria esse código? [PARTE 1](https://youtu.be/zFRUxyz7FCA), [PARTE 2](https://youtu.be/F67IG4B8oC4). 

### Depois de finalizar

Antes de passar para a próxima funcionalidade, envie o link para o diff da sua solução acessando [este formulário](https://forms.gle/zZBo1qpQioTUf5FK6)

