# Como implementar um Health Check utilizando Spring Boot Actuator?

Nesse tutorial iremos aprender como fazer nosso próprio Health Check caso for necessário.

1ª Precisamos saber qual motivação do uso do Health Check! [Aqui tem uma explicação do que entendemos que você deve considerar](../informacao_procedural/healthcheck.md)

2º Precisamos saber quais os tipos de Health Checks que existem! [Aqui tem uma explicação do que entendemos que você deve considerar](../informacao_procedural/readiness_checks.md)

Eba! Estamos contextualizados e prontos para por em prática nosso conhecimento sobre esse tema! Vamos lá?

1º Precisamos criar nossa classe que irá representar o Health Check desejado, conforme código abaixo:

```java
public class MeuHealthCheck {
    // Código omitido
}

```

# Informação de Suporte

Gostaria de saber mais sobre Health Check no Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#writing-custom-healthindicators)

Gostaria de saber sobre os Health Checks implementados pelo Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-health-indicators)