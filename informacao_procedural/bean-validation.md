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

## Anotações de validação

#### [@AssertFalse](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/AssertFalse.html)

Verifica se o campo é falso, em caso de verdadeiro, ocorre um erro.

#### [@AssertTrue](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/AssertTrue.html)

Verifica se o campo é verdadeiro, em caso de falso, ocorre um erro.

#### [@Max](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Max.html)

Verifica se o número é menor ou igual ao definido, se não, ocorre um erro.

#### [@Min](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Min.html)

Verifica se o número é maior ou igual ao definido, se não, ocorre um erro.

#### [@DecimalMax](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/DecimalMax.html)

Verifica se o número é menor ou igual ao definido, se não, ocorre um erro.

#### [@DecimalMin](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/DecimalMin.html)

Verifica se o número é maior ou igual ao definido, se não, ocorre um erro.

#### [@Future](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Future.html)

Verifica se a data está no futuro, se não, ocorre um erro.

#### [@FutureOrPresent](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/FutureOrPresent.html)

Verifica se a data está no passado ou presente, se não, ocorre um erro.

#### [@Past](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Past.html)

Verifica se a data está no passado, se não, ocorre um erro.

#### [@PastOrPresent](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/PastOrPresent.html)

Verifica se a data está no futuro ou presente, se não, ocorre um erro.

#### [@Positive](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Positive.html)

Verifica se o número é positivo, se não, ocorre um erro.

#### [@PositiveOrZero](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/PositiveOrZero.html)

Verifica se o número é positivo ou zero, se não, ocorre um erro.

#### [@Negative](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Negative.html)

Verifica se o número é negativo, se não, ocorre um erro.

#### [@NegativeOrZero](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/NegativeOrZero.html)

Verifica se o número é negativo ou zero, se não, ocorre um erro.

#### [@Null](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Null.html)

Verifica se o campo está nullo, se não, se não, ocorre um erro.

#### [@NotNull](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/NotNull.html)

Verifica se o campo não está nullo, se não, se não, ocorre um erro.

#### [@NotBlank](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/NotBlank.html)

Verifica se o campo não é nulo e vazio, se não, ocorre um erro.

#### [@NotEmpty](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/NotEmpty.html)

Verifica se a lista não está vazia ou nulla, se não, ocorre um erro.

#### [@Digits](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Digits.html)

Verifica se o número está no range definido, se não, ocorre um erro.

#### [@Email](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Email.html)

Verifica se o campo é um email válido, se não, ocorre um erro.

#### [@Pattern](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Pattern.html)

Verifica se o campo atende o REGEX definido, se não, ocorre um erro.

#### [@Size](https://javaee.github.io/javaee-spec/javadocs/javax/validation/constraints/Size.html)

Verifica se o campo atende o minimo e máximo de tamanho definido, se não, ocorre um erro.

## Qual diferença do @Valid e @Validated


## Validando classes internas

# Referências

[Validação com Bean Validation](https://blog.algaworks.com/validacao-com-bean-validation/)

# FIXME - Luram - Bean Validation
# FIXME - Luram - Bean Validation Spring