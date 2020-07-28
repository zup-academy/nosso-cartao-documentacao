# Spring Data

[Spring Data](https://spring.io/projects/spring-data) é um dos projetos do [Spring](https://spring.io/) que tem como 
objetivo prover uma forma consistente de acesso ao dados, ou seja, acesso aos banco de dados.

As suas principais funcionalidades são:

- Repositórios poderosos e abstrações de mapeamento de objetos
- Derivação dinâmica de consulta de nomes de métodos de repositório
- Suporte para auditoria transparente (criada, alterada pela última vez)

Como o objetivo do [Spring Data](https://spring.io/projects/spring-data) é prover uma forma consistente de acesso ao 
dados, existem inúmeros módulos implementados:

- [Spring Data JDBC](https://spring.io/projects/spring-data-jdbc): Suporte ao [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).
- [Spring Data JPA](https://spring.io/projects/spring-data-jpa): Suporte ao [Java Persistence API (JPA)](https://www.oracle.com/java/technologies/persistence-jsp.html).
- [Spring Data MongoDB](https://spring.io/projects/spring-data-mongodb): Suporte ao [MongoDB](https://www.mongodb.com/).

## Como configurar meu projeto?

Para configurar o módulo ou projeto do Spring é necessário mapear a dependência no `pom.xml` do seu [Maven](https://maven.apache.org/what-is-maven.html)
, conforme código abaixo:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
    <version>2.3.0.RELEASE</version>
</dependency>
```

Além de configurar seu projeto, você precisa adicionar a dependência do driver do banco escolhido, como por exemplo:

**PostgreSQL**

```
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.2.12</version>
</dependency>
```

**MySQL**

```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.20</version>
</dependency>
```

Após configurar suas dependências é necessário configurar os acessos, para tal, acesse o arquivo `application.properties` 
ou `application.yaml` e adiciona as seguintes properties:

```
spring.datasource.platform=postgres
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasourcepassword=postgres
spring.jpa.hibernate.ddl-auto=update
```

Quer saber mais sobre as propriedades do Spring Data, [clique aqui!](https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html#data-properties)

## Como declarar meu repositório