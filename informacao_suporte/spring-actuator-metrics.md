# Como configurar métricas no Spring Boot Actuator?

O Spring Boot Actuator fornece gerenciamento de dependência e configuração automática para o [Micrometer](https://micrometer.io/)
, uma biblioteca de métricas de aplicativos que suporta vários sistemas de monitoramento, incluindo:

- [Prometheus](https://prometheus.io/)
- [Datadog](https://docs.datadoghq.com/metrics/)
- [Dynatrace](https://www.dynatrace.com/)

Dentre outros, gostaria de saber a lista completa? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-metrics)

Já sabemos que o Spring em conjunto com o Micrometer, suporta vários sistemas de monitoramento de métrica, para 
habilitados, precisamos adicionar a dependência dos desejados, como por exemplo o Prometheus!

Para habilitar um endpoint que exporta métrica no formato prometheus, precisamos adicionar a seguinte dependência no 
arquivo `pom.xml`, conforme exemplo abaixo:

```xml
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
</dependency>
```

Está quase tudo pronto, temos que habilitar o endpoint `/actuator/prometheus` para isso, vamos adicionar a seguinte 
propriedade no arquivo `application.properties`, conforme exemplo abaixo:

```properties
management.endpoints.web.exposure.include=info,health,prometheus
management.endpoints.prometheus.enabled=true
```

Eba, está tudo configurado! Vamos testar?

Para testar, basta abrir seu navegador e chamar o endereço `http://localhost:8080/actuator/prometheus`!

Deu tudo certo!? Nossa aplicação agora está expondo sua métrica! 

Digamos que entramos em contato com o time de operação \ sustentação para informar que a sua aplicação está pronta para 
ser monitorada, e tivemos um retorno do time, dizendo que precisamos adicionar uma LABEL com o nome da aplicação e qual 
ambiente.

Talvez esteja pensando, o que é LABEL? Não se preocupe! [Aqui tem uma explicação do que entendemos que você deve considerar](https://prometheus.io/docs/practices/naming/)

No material anterior você aprendeu sobre o formato de métrica do Prometheus, vamos recapitular?

- NAME é o nome da métrica, como por exemplo: `proposta_criadas_total`
- LABEL é utilizado para diferenciar as características da métrica, como por exemplo:

`proposta_criadas_total{aplicacao="serviço de proposta", ambiente="desenvolvimento"}`

Sabemos que essa métrica vem do serviço de proposta e do ambiente de desenvolvimento!

**Importante** 

Cuidado com a quantidade de LABEL, quanto mais, mais irá aumentar os dados armazenados no Prometheus, podendo causar 
problemas de performance e de disco.

Como por exemplo na métrica acima, a gente criou dois registros no Prometheus um para a LABEL aplicação e outra para a 
ambiente, assim você consegue fazer buscas inteligente ao troco de talvez ter problema de performance e disco, portanto,
use com parcimônia!

Agora que estamos bem contextualizados e fundamentados, vamos adicionar o nome da aplicação e o ambiente?

Para isto, o Spring provê uma forma simples e rápida via properties, conforme exemplo abaixo:

```properties
management.metrics.tags.aplicacao=serviço de proposta
management.metrics.tags.ambiente=desenvolvimento
```

Para testar, basta abrir seu navegador e chamar o endereço `http://localhost:8080/actuator/prometheus`!

Está tudo funcionando conforme esperado, porém, imagina quando a gente levar esse código para outros ambientes, como por 
exemplo: homologação, pré-produção e produção!

Vamos ter que alterar o código? Lembra do [The Twelve Factor App](https://12factor.net/pt_br/)?

Aqui também se aplica o fator III. Configurações, na qual diz que você deve armazenar as configurações no ambiente!

* Talvez não esteja se recordando, não tem problema! [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/twelve-factor-config.md)

Vamos aplicá-los?

```properties
management.metrics.tags.aplicacao=${NOME_DA_APLICACAO:serviço de proposta}
management.metrics.tags.ambiente=${AMBIENTE:desenvolvimento}
```

Demais né! Lembre-se de ler abaixo sobre segurança é extremamente importante!

## Dicas de Luram Archanjo

Não deixe pública sua API, alinhe sempre com sua equipe as melhores práticas, como por exemplo:

- Adicionar autenticação
- Adicionar autorização

## Dicas de Claudio Eduardo Oliveira

Não negligencie as informações que você está expondo sobre a sua infraestrutura.

# Informação de Suporte

Está em dúvida de como configurar o Spring Boot Actuator? [Aqui você encontra como fazer isto!](../informacao_suporte/spring-actuator.md)

Talvez esteja pensando sobre segurança no Spring Boot Actuator? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_suporte/spring-actuator-security.md)

Quer saber mais sobre Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-enabling)

Quer saber mais sobre o The Twelve-Factor App? Acesse o [link!](https://12factor.net/pt_br/)
