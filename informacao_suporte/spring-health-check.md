# Como implementar um Health Check utilizando Spring Boot Actuator?

Neste tutorial vamos aprender como fazer nosso próprio Health Check caso for necessário.

1º Precisamos saber qual a motivação do uso do Health Check! [Aqui tem uma explicação do que entendemos que você deve considerar](../informacao_procedural/healthcheck.md)

2º Precisamos saber quais os tipos de Health Checks que existem! [Aqui tem uma explicação do que entendemos que você deve considerar](../informacao_procedural/readiness_checks.md)

Eba! Estamos contextualizados e prontos para pôr em prática nosso conhecimento sobre esse tema! Vamos lá?

1º Precisamos criar nossa classe que irá representar o Health Check desejado, conforme código abaixo:


```java
public class MeuHealthCheck {
    // Código omitido
}
```

2º Precisamos implementar a interface [HealthIndicator](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/actuate/health/HealthIndicator.html) 
que o Spring Boot Actuator nos provê, conforme código abaixo:

```java
public class MeuHealthCheck implements HealthIndicator {

    @Override
    public Health health() {
        // TODO Precisamos implementar o método
        return null;
    }

}
```

Ao implementar essa interface, precisamos implementar o método `health` no qual é necessário retornar o objeto [Health](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/actuate/health/Health.html).

Este objeto é bastante simples, você precisa passar qual [status](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/actuate/health/Status.html) 
do Health Check, como por exemplo

- **DOWN:** Status indicando que o componente ou subsistema sofreu uma falha inesperada.
- **OUT_OF_SERVICE:** Status indicando que o componente ou subsistema foi retirado de serviço e não deve ser usado.
- **UNKNOWN:**  Status indicando que o componente ou subsistema está em um estado desconhecido.
- **UP:** Status indicando que o componente ou subsistema está funcionando conforme o esperado.

Caso necessário, você pode passar detalhes do seu Health Check, como por exemplo:

- Versão
- Descrição
- IP

Muito legal né? Vamos implementar?

```java
public class MeuHealthCheck implements HealthIndicator {

    @Override
    public Health health() {
        Map<String, Object> details = new HashMap<>();
        details.put("versão", "1.2.3");
        details.put("descrição", "Meu primeiro Health Check customizado!");
        details.put("endereço", "127.0.0.1");
        
        return Health.status(Status.UP).withDetails(details).build();
    }

}
```

E para finalizar, precisamos dizer para o Spring Boot considerar essa implementação, para isto, precisamos adicionar a 
anotação [@Component](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Component.html)
, conforme código abaixo:

```java
@Component
public class MeuHealthCheck implements HealthIndicator {
    // Código omitido
}
```

Pronto! Criamos nosso primeiro Health Check customizado utilizando Spring Boot Actuator!

Para testar, basta abrir seu navegador e chamar o endereço `http://localhost:8080/actuator/health`!

## Informação de Suporte

Gostaria de saber mais sobre Health Check no Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#writing-custom-healthindicators)

Gostaria de saber sobre os Health Checks implementados pelo Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-health-indicators)
