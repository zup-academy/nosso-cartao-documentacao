# Padronização de erros seguindo as boas práticas de Orientação a Objetos?

Estamos construíndo um produto de geração de cartão, transação, etc. E algum parceiro tanto interno quanto externo gostaria 
de se integrar com a gente, ou seja, gostaria de usar nossas APIs e para que a integração seja o mais eficiente possível 
precisamos enriquecer nossas APIs com detalhes, inclusive no cenário de erro!

Portanto, precisamos fornecer o máximo possível de informação para que o parceiro identifique o que ele 
está fazendo de errado e consiga corrigir!

Ponto importante, quando falamos de enriquecer nossas APIs com o máximo de informação possível, lembre-se sempre da 
segurança, como por exemplo o erro `Número de cartão não existe`.

Quando um Hacker vê esse tipo de mensagem, ele pensa, vou ficar tentando um monte de número. Quando parar de dar esse 
erro, sei que é um número de cartão válido, o resto é história.

Estamos bem contextualizados, certo!?

Ainda não, quando falamos de APIs precisamos definir um modelo único de erro, para que seja uniforme em todas as APIs, 
assim o parceiro tem uma sensação de familiaridade e fica muito mais fácil outro sistema se integrar com o nosso produto!

Imagina só! Termos 10 APIs cada uma com um formato de erro diferente!

# Vamos fazer isso com Spring, então!
  
# Informação de Suporte

Gostaria de saber a padronização de erros utilizada pelo Spring Boot? [Aqui você encontra como fazer isso !!!](error-spring.md)

Gostaria de saber a padronização de erros utilizada pela Zup? [Aqui você encontra como fazer isso !!!](../informacao_suporte/error-zup.md)

Quer sabemos mais sobre Handler Advice, acesse o [link!](https://spring.io/blog/2013/11/01/exception-handling-in-spring-mvc)