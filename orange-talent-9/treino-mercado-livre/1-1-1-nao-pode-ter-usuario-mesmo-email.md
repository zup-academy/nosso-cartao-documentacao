# Não podemos ter dois usuários com o mesmo email.

### Necessidades

*   Só pode existir um usuário com o mesmo email.

### Resultado esperado

*   Status 400 informando que não foi possível realizar um cadastro com este email.

### Antes de começar

Por favor descreva como você pretende realizar a implementação deste desafio. 
  
  **Para acessar o formulário [clique aqui](https://forms.gle/CsLKcN3rGYY9oT5v7)**


### **Informações de suporte geral**

1.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://youtu.be/SygOC4d_N5w)

2.  Aqui provavelmente você terá um if em algum lugar para verificar a existência de um outro autor. Todo código que tem uma branch de código(if,else) tem mais chance de executar de maneira equivocada. Tente criar um teste automatizado para aumentar ainda mais a confiabilidade do seu código. [Criamos testes automatizados para que ele nos ajude a revelar e consertar bugs na aplicação.​](https://youtu.be/vCnhwbkX3EA)[

3.  Como Alberto fez esse código? [Query direto na classe de validação /o\.](https://youtu.be/PLrRFyMDBpY)

4.  Como Alberto fez esse código [usando um Repository na classe de validação.](https://youtu.be/Wn-dk9yTids)

5. [Como ficaram os testes?](https://youtu.be/AQEgmiqt2pw)

### Informações de suporte para a combinação Java/Kotlin + Spring

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/H6aM-4RaRrE)

### Depois de finalizar
Antes de passar para a próxima funcionalidade, **envie o link para o diff da sua solução acessando [este formulário](https://forms.gle/CX8L1j1KRwaSzXZP7)**


