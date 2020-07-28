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

## Como mapear minha entidade?

Neste tutorial, iremos ver como mapear uma entidade utilizando o [Java Persistence API (JPA)](https://www.oracle.com/java/technologies/persistence-jsp.html), 
caso deseja mapear utilizando outro módulo, como o [MongoDB](https://www.mongodb.com/), por favor, acesse o [link!](https://emmanuelneri.com.br/2017/04/17/utilizando-mongodb-com-spring-data-e-spring-boot/)

Para mapear nossa entidade, precisamos utilizar algumas anotações, como por exemplo:

#### @Entity

Anotação utilizada para especificar que a classe é uma representação de uma entidade em nosso banco de dados, conforme 
código abaixo:

```
@Entity
public class Carro {
    // Código omitido
}
```

#### @Id

Anotação utilizada para especificar o identificador da nossa entidade, conforme código abaixo:

```
@Id
@GeneratedValue(generator = "UUID")
@GenericGenerator(name = "UUID", strategy = "org.hibernate.id.UUIDGenerator")
private String id;
```

#### @Column

Anotação utilizada para especificar uma coluna da nossa entidade e seu tipo, conforme código abaixo:

```
@Column(nullable = false)
private String nome;
```

Nesse caso, dependendo do seu banco de dados, será criado uma coluna do tipo VARCHAR(255), pois o atributo é String, 
quer saber mais do mapeamento de tipo de atributo x tipo no banco de dados, acess o [link!](https://www.tutorialspoint.com/hibernate/hibernate_mapping_types.htm#:~:text=When%20you%20prepare%20a%20Hibernate,not%20SQL%20database%20types%20either.)

#### @Enumerated

Anotação utilizada para especificar que um atributo de entidade representa um tipo enumerado, conforme código abaixo:

```
@Enumerated
private TipoEnum tipo;
```

#### @Temporal

Anotação utilizada para especificar que um atributo de entidade representa uma data, conforme código abaixo:

```
@Temporal(TemporalType.DATE)
private LocalDate data;

@Temporal(TemporalType.TIME)
private LocalDateTime hora;

@Temporal(TemporalType.TIMESTAMP)
private LocalDateTime dataEhora;
```

#### @OneToMany

Anotação utilizada para especificar um relacionamento de banco de dados um para muitos, conforme código abaixo:

```
@OneToMany
private Collection<Pneu> pneus = new ArrayList<>();
```

#### @ManyToOne

Anotação utilizada para especificar um relacionamento de banco de dados muitos para um, conforme código abaixo:

```
@ManyToOne
private Pessoa pessoa;
```

#### @ManyToMany

Anotação utilizada para especificar um relacionamento de banco de dados muitos para muitos, conforme código abaixo:

```
@ManyToMany
private Collection<Pessoa> donos = new ArrayList<>();
```

#### @OneToOne

Anotação utilizada para especificar um relacionamento de banco de dados um para um, conforme código abaixo:

```
@OneToOne
private Montadora montadora;
```

Quer saber mais sobre as notações do JPA, acesso o [link!](https://dzone.com/articles/all-jpa-annotations-mapping-annotations)

## Como declarar meu repositório?