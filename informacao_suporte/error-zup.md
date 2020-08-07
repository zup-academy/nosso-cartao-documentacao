# Padronização de erros utilizada pela Zup?

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
  
O Spring fornece uma forma de tratar todos os erros não tratados que aconteceram na camada da nossa API, ou seja, no 
nosso Controller.

Vamos começar?

**1º** Precisamos definir como será o erro padrão em nossas APIs, aqui é apenas uma sugestão, no cenário real, devemos alinhar 
com nossos(as) companheiros(as) de equipe!

```java
public class ErroPadronizado {

    private Collection<String> mensagens;

    // Getters, setters, construtor omitidos
}
```

Essa classe convertida em [JSON](https://www.json.org/json-en.html), ficaria assim:

```json
{
  "mensagens": [
    "Campo documento must not be blank",
    "Campo salario must not be null"
  ]
}
```

Muito intuitivo né!?

**2º** Precisamos criar nossa classe que irá tratar todos os erros não tratados que aconteceram na camada da nossa API.

```java
public class MeuHandlerAdvice {
    // Código omitido
}
```

Quando falamos de lidar com exceções no Spring é utilizado `HandlerAdvice`, portanto sugiro, colocar o nome como sufixo, 
conforme código acima.

**3º** Precisamos dizer para o Spring que está classe é um `HandlerAdvice`, principalmente de APIs, para tal, precisamos 
adicionar a seguinte anotação [@RestControllerAdvice](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/bind/annotation/RestControllerAdvice.html) 
em nossa classe, conforme código abaixo:

```java
@RestControllerAdvice
public class MeuHandlerAdvice {
    // Código omitido
}
```

**4** Está tudo configurado, agora precisamos começar dar inteligência para o nosso `HandlerAdvice`!

Vamos começar tratando os erros de [Bean Validation](../informacao_suporte/bean-validation.md)?

Quando é violado alguma restrição do Bean Validation, é lançado a exceção [MethodArgumentNotValidException](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/MethodArgumentNotValidException.html).

Então é ela que precisamos tratar! Para isto o Spring fornece o anotação [@ExceptionHandler](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/ExceptionHandler.html)

Vamos criar nosso método e tratar essa exceção?

```java
@RestControllerAdvice
public class MeuHandlerAdvice {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErroPadronizado> handle(MethodArgumentNotValidException methodArgumentNotValidException) {
        Collection<String> mensagens = new ArrayList<>();
        BindingResult bindingResult = methodArgumentNotValidException.getBindingResult();
        List<FieldError> fieldErrors = bindingResult.getFieldErrors();
        fieldErrors.forEach(fieldError -> {
            String message = String.format("Campo %s %s", fieldError.getField(), fieldError.getDefaultMessage());
            mensagens.add(message);
        });

        ErroPadronizado erroPadronizado = new ErroPadronizado(mensagens);
        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(erroPadronizado);
    }

}
```

Pronto! Nesse trecho de código acima, estamos tratando e recebendo a exceção MethodArgumentNotValidException no parâmetro, 
pois o Spring irá passar como parâmetro para a gente, demais né!?

E a partir do momento que temos a exceção, podemos usufruir da mesma, como por exemplo no código acima, que estamos 
pegando todos os campos que deram erro e formatando de acordo com o erro padrão:

```json
{
  "mensagens": [
    "Campo documento must not be blank",
    "Campo salario must not be null"
  ]
}
```

Demais né!?

Mas e os outros casos de uso, como por exemplo [422](../informacao_suporte/rest-422.md)!

Neste caso, caso tenha uma a exceção específica na qual não foi tratada e chegou na camada de controller, precisamos 
tratar a mesma, como por exemplo a exceção `ContaBloquedaException`.

Nesse cenário, gostaríamos de retornar 422! Vamos lá?

```java
@ExceptionHandler(ContaBloquedaException.class)
public ResponseEntity<ErroPadronizado> handle(ContaBloquedaException contaBloquedaException) {
    Collection<String> mensagens = new ArrayList<>();
    
    // Trata sua exceção

    ErroPadronizado erroPadronizado = new ErroPadronizado(mensagens);
    return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(erroPadronizado);
}
```

Demais né!? Mas temos um problema! Eu vou ter que ficar criando uma tratativa por exceção, isso é muito ruim!

Visando isso, vamos criar uma exceção de API? Que tenha o status code desejado e a mensagem de erro?

```java
public class ApiErroException extends RuntimeException {

    private final HttpStatus httpStatus;

    private final String reason;

    public ApiErroException(HttpStatus httpStatus, String reason) {
        super(reason);
        this.httpStatus = httpStatus;
        this.reason = reason;
    }

    // Getters, setters, construtor omitidos

}
```

Assim agora, quando a gente quiser gerar um erro na API precisamos somente lançar essa exceção e adicionar somente uma 
tratativa no `HandlerAdvice`, conforme código abaixo:

```java
@ExceptionHandler(ApiErroException.class)
public ResponseEntity<ErroPadronizado> handleApiErroException(ApiErroException apiErroException) {
    Collection<String> mensagens = new ArrayList<>();
    mensagens.add(apiErroException.getReason());

    ErroPadronizado erroPadronizado = new ErroPadronizado(mensagens);
    return ResponseEntity.status(apiErroException.getHttpStatus()).body(erroPadronizado);
}
```

Demais né!?

# Dicas de Luram Archanjo

Está é uma pratica utilizada pela Zup e outras empresas, porém acarreta outros problemas, como por exemplo:

- Criação de inúmeras exceções
- Tratativa de inúmeras exceções
- Violação do objetivo da Exceção que é ser utilizada para indicar um erro e ser tratada e não ser utilizada para indicar 
um determinado erro de API.
- Violação das camadas, pois você pode lançar ela de qualquer lugar, como por exemplo: Service e Repository.

Lembre-se, devemos alinhar com nossos(as) companheiros(as) de equipe!

# Informação de Suporte

Gostaria de saber a padronização de erros utilizada pelo Spring Boot? [Aqui você encontra como fazer isso !!!](error-spring.md)

Gostaria de saber a padronização de erros seguindo as boas práticas de Orientação a Objetos? [Aqui você encontra como fazer isso !!!](error-object-oriented.md)

Quer sabemos mais sobre Handler Advice, acesse o [link!](https://spring.io/blog/2013/11/01/exception-handling-in-spring-mvc)