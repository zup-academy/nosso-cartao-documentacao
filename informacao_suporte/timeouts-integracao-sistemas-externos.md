## Recomendação: Toda execução externa deve ter um tempo máximo de resposta

Controlar o tempo máximo de espera de resposta para os possíveis tipos de comunicação que seu sistema pode ter, gera um pouco mais de previsibilidade na execução do código necessário para atender determinada requisição. Independente do ecossistema de tecnologias que você esteja lidando, é recomendado que você controle este tempo de resposta. 

### Controlando timeouts do Feign para aplicações Spring Boot

Em aplicações que utilizam Spring Boot, estas possibilidades de configuração já vem prontas através das classes de autoconfiguração providas pelos starters. Por exemplo, para controlar o tempo de espera para requisições feitas através do Feign:

```
feign.client.config.nomeFeignClienteDefinidoNoBean.read-timeout=100
```
Agora toda comunicação feita através do Feign, para aquele bean específico, o tempo máximo de espera da resposta vai ser de 100 milissegundos. Você também pode configurar o tempo máximo para conseguir realizar a conexão com o outro sistema:

```
feign.client.config.nomeFeignClienteDefinidoNoBean.connect-timeout=100
```

A combinação acima leva a uma espera máxima de 200 milissegundos para a execução da operação. Você pode saber mais sobre as possibilidades de configuração do Feign num projeto Spring Boot consultando a [documentação oficial](https://docs.spring.io/spring-cloud-openfeign/docs/2.2.4.RELEASE/reference/html/appendix.html)

### Controlando timeouts do Hibernate para aplicações Spring Boot

O mesmo tipo de approach pode ser utilizado para controlar o timeout de execução padrão de queries através de alguma implementação da JPA. 

```
spring.jpa.properties.javax.persistence.query.timeout = 50
```
Agora você sabe que por default toda query só pode levar no máximo 50 milissegundos. Caso em algum ponto do sistema este tempo não seja suficiente, é possível trocar através dos chamados hints da JPA. Tem referências na documentação do [Spring Data JPA](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-hints). Você também pode encontrar referências neste [texto escrito por Vlad Mihalcea, um commiter do Hibernate e pessoa com muita autoridade para falar sobre o assunto](https://vladmihalcea.com/jpa-hibernate-query-hints/). [No exemplo 469, na documentação do Hibernate você também encontra um exemplo](https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#jpql-api)


