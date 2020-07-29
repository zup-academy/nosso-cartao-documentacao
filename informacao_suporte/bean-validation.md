# Bean Validation

Bean Validation é uma especificação que permite validar objetos com facilidade em diferentes camadas da aplicação. 
A vantagem de usar Bean Validation é que as restrições ficam inseridas nas classes de modelo.

De acordo com a [documentação](https://docs.spring.io/spring/docs/4.1.x/spring-framework-reference/html/validation.html#validation-beanvalidation) 
do Spring, a implementação padrão utilizada é a [Hibernate Validator](http://hibernate.org/validator/).

## Como utilizar

No Spring para efetuar validações, deve-se anotar o classe, método ou parâmetro com a anotação 
[@Validated](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/validation/annotation/Validated.html)
ou [@Valid](https://docs.oracle.com/javaee/7/api/javax/validation/Valid.html).

```
@PostMapping
public Response post(@Validated @RequestBody Body body) {
    ...
}
```

Após anotar a classe, método ou parâmetro com a anotação @Validated ou @Valid precisamos colocar os validadores nos 
atributos desejados, conforme código abaixo:

```java
public class Pessoa {

    @NotBlank
    private String nome;

    @NotNull
    @Positive
    private Integer idade;

}
```

Pronto! Temos uma classe que será validada, caso for violado alguma restrição será gerado a exception [MethodArgumentNotValidException](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/MethodArgumentNotValidException.html).

Quer saber mais sobre as anotações, acesse o [link!](https://docs.oracle.com/javaee/7/api/javax/validation/constraints/package-summary.html)