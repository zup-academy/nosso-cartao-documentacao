# Como configurar o Spring Boot Actuator?

O Spring Boot Actuator inclui vários recursos adicionais para ajudá-lo a monitorar e gerenciar seu aplicativo quando 
você o envia à produção, como por exemplo:

- Endpoint para monitoramento da saúde da aplicação (Health Check).
- Endpoint para expor métricas da aplicação.
- Endpoint para expor as propriedades da sua aplicação.

Super legal né! Quer saber quais são os outros endpoints, acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-endpoints)

Vamos configurar!?

1º Precisamos adicionar a seguinte dependência em seu arquivo `pom.xml`:

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-actuator</artifactId>
	</dependency>
</dependencies>
```

2º Precisamos verificar se está tudo configurado, para isso abra em seu navegador o seguinte endereço:

`http://localhost:8080/actuator`

Neste endpoint irá listar todos os endpoints configurados, como por exemplo:

```
# Endpoint para monitoramento da saúde da aplicação (Health Check)

http://localhost:8080/actuator/health
```

Eba! Está tudo OK!

Sim, mas antes de continuar com sua tarefa, aconselhamos dar uma lida no tópico abaixo, sobre segurança!

# Configurando métricas

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

# Configurando segurança

O Spring Boot Actuator fornece muitas APIs interessantes para monitoramento do nosso sistema, contrapartida, essas 
informações podem ser utilizadas para explorar falhas de segurança!

Como assim!?

Vou dar um exemplo, imagina que por algum motivo o recurso de `/actuator/env` está público, ou seja, qualquer um pode 
acesso de qualquer lugar!

Um Hacker, pode por exemplo obter todas as versões das dependências utilizadas no seu projeto e 
explorar falhas, como por exemplo na imagem abaixo:

![alt text](../images/spring-008.png "Spring Boot Actuator")

O Hacker sabe que estou utilizando Spring Boot 2.3.0 e com uma simples pesquisa no google pode encontrar falhas 
relacionadas a esta versão, como por exemplo na imagem abaixo:

![alt text](../images/spring-009.png "Spring Boot Actuator")

Este tópico é bastante importante para todos os projetos da Zup, portanto vamos falar de segurança?

* Gostaria de saber mais sobre segurança? [Aqui tem uma explicação do que entendemos que você deve considerar](../informacao_procedural/seguranca_cloud_native.md)

## Utilizando somente o necessário!

Sabemos que no Spring Boot Actuator existem vários Endpoints e que alguns podem expor informações sensíveis!

Como eu posso remover ou desabilitar meus endpoints?

Existem duas alternativas!

1º Habilitar somente o que é utilizado, para isto é necessário adicionar a propriedade:

`management.endpoints.web.exposure.include=health,metrics,prometheus` 

2º Remover os não utilizados, para isto é necessário adicionar a propriedade:

`management.endpoints.web.exposure.exclude=env,beans`

## Utilizando CORS!

O CORS (Cross-origin Resource Sharing) é um mecanismo utilizado pelos navegadores para compartilhar recursos entre 
diferentes origens. O CORS é uma especificação do W3C e faz uso de headers do HTTP para informar aos navegadores se 
determinado recurso pode ser ou não acessado.

Permitindo receber somente de uma origem, aumenta demais a segurança das APIs do Spring Boot Actuator!

Para isto, basta adicionar as seguintes propriedades no arquivo `application.properties`:

```properties
management.endpoints.web.cors.allowed-origins=https://example.com
management.endpoints.web.cors.allowed-methods=GET
```

# Dicas de Luram Archanjo

Não deixe pública sua API, alinhe sempre com sua equipe as melhores práticas, como por exemplo:

- Adicionar autenticação
- Adicionar autorização

# Dicas de Cláudio

Não negligencie as informações que você está expondo sobre a sua infraestrutura.

# Informação de Suporte

Quer saber mais sobre Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-enabling)

Quer saber mais sobre o The Twelve-Factor App? Acesse o [link!](https://12factor.net/pt_br/)