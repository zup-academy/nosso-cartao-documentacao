# Não podemos ter dois usuários com o mesmo email.

## Necessidades

*   Só pode existir um usuário com o mesmo email.

## Resultado esperado

*   Status 400 informando que não foi possível realizar um cadastro com este email.

## Informações de suporte geral**

1.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://youtu.be/YXF8Ll64tfk)
2.  Aqui provavelmente você terá um if em algum lugar para verificar a existência de um outro autor. Todo código que tem uma branch de código(if,else) tem mais chance de executar de maneira equivocada. Tente criar um teste automatizado para aumentar ainda mais a confiabilidade do seu código. [Criamos testes automatizados para que ele nos ajude a revelar e consertar bugs na aplicação.​](https://youtu.be/5kbcCsd_4Vw)[
3.  Como Alberto fez esse código? [Query direto na classe de validação /o\.](https://youtu.be/JXbZ1d0vI0s)
4.  Como Alberto fez esse código [usando um Repository na classe de validação.](https://youtu.be/-I2SXOSX16A)
5. [Como ficaram os testes?](https://youtu.be/laJV7AYOTy4)

### informações de suporte para a combinação Java/Kotlin + Spring

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/LlX6zoGwQQA)
