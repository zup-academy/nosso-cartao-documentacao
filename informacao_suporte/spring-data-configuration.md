# Como configurar meu projeto?

Para configurar o módulo ou projeto do Spring é necessário mapear a dependência no `pom.xml` do seu [Maven](https://maven.apache.org/what-is-maven.html)
, conforme código abaixo:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
    <version>2.3.0.RELEASE</version>
</dependency>
```

Além de configurar seu projeto, você precisa adicionar a dependência do driver do banco escolhido, como por exemplo:

**PostgreSQL**

```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.2.12</version>
</dependency>
```

**MySQL**

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.20</version>
</dependency>
```

Após configurar suas dependências é necessário configurar os acessos, para tal, acesse o arquivo `application.properties` 
ou `application.yaml` e adiciona as seguintes properties:

```properties
spring.datasource.platform=postgres
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.hibernate.ddl-auto=update
```

# Informação de Suporte

Quer saber mais sobre as propriedades do Spring Data? [clique aqui!](https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html#data-properties)
