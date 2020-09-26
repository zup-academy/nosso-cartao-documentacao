# Email do autor precisa ser único

## necessidades

* O email do autor precisa ser único no sistema

## resultado esperado

* Em caso de email duplicado devemos retornar 400 informando a falha. 

## informações de suporte

* [TODO FRAMEWORK MVC MINIMAMENTE MADURO POSSUI UM MECANISMO PRONTO DE REALIZAR VALIDAÇÃO CUSTOMIZADA. SPRING, NESTJS E ASP.NET CORE MVC TÊM](../informacao-suporte-design/validacao-precisa-ser-suportada-fw.md).

* Aqui provavelmente você terá um if em algum lugar para verificar a existência de um outro autor. Todo código que tem uma branch de código(if,else) tem mais chance de executar de maneira equivocada. Tente criar um teste automatizado para aumentar ainda mais a confiabilidade do seu código. [CRIAMOS TESTES AUTOMATIZADOS PARA QUE ELE NOS AJUDE A REVELAR E CONSERTAR BUGS NA APLICAÇÃO](https://sttp.site/chapters/getting-started/why-software-testing.html) 

* O material linkado acima é para o livro aberto de Mauricio Aniche. Caso você queira um vídeo em português, [confere aqui](https://youtu.be/2HxTm5th96s). 

* Utilize um insomnia ou qualquer outra forma para verificar o endpoint

* [PEGUE CADA UMA DAS CLASSES QUE VOCÊ CRIOU E REALIZE A CONTAGEM DA CARGA INTRÍNSECA](../informacao-suporte-design/treino-contagem-carga-intrinseca.md). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.

* [COMO ALBERTO FARIA ESSE CÓDIGO?](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/blob/eb6f3fec10d2801a076127cf74b2ec81cf54aeb2/src/main/java/com/deveficiente/casadocodigov2/novoautor/ProibeEmailDuplicadoAutorValidator.java) e [também aqui](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/blob/eb6f3fec10d2801a076127cf74b2ec81cf54aeb2/src/main/java/com/deveficiente/casadocodigov2/novoautor/AutoresController.java) 

## informações extras de suporte
* Para receber os dados da request como json, temos a annotation ```@RequestBody```

* Usamos a annotation ```@Valid``` para pedir que os dados da request sejam validados

* Está pensando em como fazer as validações dos dados do seu objeto? Olha que interessante, já existe um especificação no mundo Java que pensou só nisso. Ela é chamada Bean Validation. Inclusive o Spring já tem integração fina com ela. [Confere essa dica aqui](../informacao_suporte/bean-validation.md)

* [COMO CRIAR UM @RESTCONTROLLERADVICE PARA CUSTOMIZAR O JSON DE SAÍDA COM ERROS DE VALIDAÇÃO](../informacao_suporte/error-spring.md)

* [Exemplo de um ```RestControllerAdvice``` para você utilizar.](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/blob/master/src/main/java/com/deveficiente/casadocodigov2/compartilhado/ValidationErrorHandler.java) 

* [COMO EXTERNALIZAR AS MENSAGENS DE ERRO NO ARQUIVO DE CONFIGURAÇÃO](../informacao_suporte/externaliza-mensagens-properties.md)


