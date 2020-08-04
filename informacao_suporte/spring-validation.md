# Como utilizar Spring Validation?

O spring fornece um módulo de validação dos nossos objetos, denominado Spring Validation, se o seu projeto estiver 
utilizando o Spring Boot 2.3.0 ou superior, precisamos adicionar a seguinte dependência:

```xml
<dependency> 
    <groupId>org.springframework.boot</groupId> 
    <artifactId>spring-boot-starter-validation</artifactId> 
</dependency>
```

Bom!!! Já temos tudo preparado, vamos começar?

1º Precisamos criar nossa classe de validação, conforme o código abaixo:

```java
public class MeuValidador implements Validator {
    
}
```

2º Precisamos implementar a interface [Validator](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/validation/Validator.html)

* Dica: O importe deve ser `org.springframework.validation.Validator`

```java
public class MeuValidador implements Validator {

    @Override
    public boolean supports(Class<?> aClass) {
        return false;
    }

    @Override
    public void validate(Object o, Errors errors) {

    }

}
```

3º Já temos tudo configurado, agora é hora de implementar os métodos `supports` e `validate`, vamos começar pelo `supports`

O método `supports` tem como objetivo determinar para qual classe esse validador deve ser aplicado, como por exemplo:

```java
@Override
public boolean supports(Class<?> aClass) {
    return NovaPropostaRequest.class.equals(aClass);
}
```

4º Já configuramos para qual classe esse validador se aplica, agora é hora de implementar nossas validações!

```java
@Override
public void validate(Object object, Errors errors) {
    final NovaPropostaRequest request = (NovaPropostaRequest) object;    
    //se essa proposta está com um documento invalido. Como pode fazer isso?
        errors.rejectValue("documento", "Documento inválido");
    //fecha condicao
}
```

5º Já temos tudo pronto! Agora precisamos dizer para o Spring utilizar o mesmo, para isto basta anotar a classe do validador 
com a anotação [@Component](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Component.html).

```java
@Component
public class MeuValidador implements Validator {
    // Código omitido
}
```

E para finalizar, precisamos e adicionar quais validadores nosso controller irá aplicar, conforme código abaixo:

```java
@RestController
public class MeuController {

    @Autowired
    private MeuValidador meuValidador;

    @InitBinder
    private void initBinder(WebDataBinder binder) {
        binder.addValidators(meuValidador);
    }

}
```

Eba! Já temos validações!!!

# Informação de Suporte

Quer saber mais sobre Spring Validation, acesse o [link!](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#validator)