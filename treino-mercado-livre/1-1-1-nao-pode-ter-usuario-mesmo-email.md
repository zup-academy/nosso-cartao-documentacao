# Não podemos ter dois usuários com o mesmo email.

## Necessidades

*   Só pode existir um usuário com o mesmo email.

## Resultado esperado

*   Status 400 informando que não foi possível realizar um cadastro com este email.

## Informações de suporte geral**

1.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://drive.google.com/file/d/1wc5ChsPeGFjqypb9QI7tGRMl9dn0WkkL/view?usp=sharing)
2.  Aqui provavelmente você terá um if em algum lugar para verificar a existência de um outro autor. Todo código que tem uma branch de código(if,else) tem mais chance de executar de maneira equivocada. Tente criar um teste automatizado para aumentar ainda mais a confiabilidade do seu código. [Criamos testes automatizados para que ele nos ajude a revelar e consertar bugs na aplicação.​](https://drive.google.com/file/d/1SAvODkuAVuvM5Bm4cNp2W0Aes59GI-Eq/view?usp=sharing)[
3.  Como Alberto fez esse código? [Query direto na classe de validação /o\.](https://drive.google.com/file/d/1HLkB8Q1L6wLRk4RQwbXDnbv2GSUJ8c0V/view?usp=sharing)
4.  Como Alberto fez esse código [usando um Repository na classe de validação.](https://drive.google.com/file/d/1R3Ot8Mxi5qwq5ga5vQbw4wsP945JPMKg/view?usp=sharing)

### informações de suporte para a combinação Java/Kotlin + Spring

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://drive.google.com/file/d/18q7IUF1EmeGrPFAab1CHIXP3COf5KNHd/view?usp=sharing)