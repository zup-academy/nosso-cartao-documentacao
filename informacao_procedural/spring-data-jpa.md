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

```java
@Entity
public class Carro {
    // Código omitido
}
```

#### @Id

Anotação utilizada para especificar o identificador da nossa entidade, conforme código abaixo:

```java
public class MinhaEntidade {

    @Id
    @GeneratedValue(generator = "UUID")
    @GenericGenerator(name = "UUID", strategy = "org.hibernate.id.UUIDGenerator")
    private String id;

}
```

#### @Column

Anotação utilizada para especificar uma coluna da nossa entidade e seu tipo, conforme código abaixo:

```java
public class MinhaEntidade {
    
    @Column(nullable = false)
    private String nome;

}
```

Nesse caso, dependendo do seu banco de dados, será criado uma coluna do tipo VARCHAR(255), pois o atributo é String, 
quer saber mais do mapeamento de tipo de atributo x tipo no banco de dados, acess o [link!](https://www.tutorialspoint.com/hibernate/hibernate_mapping_types.htm#:~:text=When%20you%20prepare%20a%20Hibernate,not%20SQL%20database%20types%20either.)

#### @Enumerated

Anotação utilizada para especificar que um atributo de entidade representa um tipo enumerado, conforme código abaixo:

```java
public class MinhaEntidade {

    @Enumerated
    private TipoEnum tipo;

}
```

#### @Temporal

Anotação utilizada para especificar que um atributo de entidade representa uma data, conforme código abaixo:

```java
public class MinhaEntidade {
    
    @Temporal(TemporalType.DATE)
    private LocalDate data;
    
    @Temporal(TemporalType.TIME)
    private LocalDateTime hora;
    
    @Temporal(TemporalType.TIMESTAMP)
    private LocalDateTime dataEhora;

}
```

#### @OneToMany

Anotação utilizada para especificar um relacionamento de banco de dados um para muitos, conforme código abaixo:

```java
public class MinhaEntidade {
    
    @OneToMany
    private Collection<Pneu> pneus = new ArrayList<>();

}
```

#### @ManyToOne

Anotação utilizada para especificar um relacionamento de banco de dados muitos para um, conforme código abaixo:

```java
public class MinhaEntidade {

    @ManyToOne
    private Pessoa pessoa;

}
```

#### @ManyToMany

Anotação utilizada para especificar um relacionamento de banco de dados muitos para muitos, conforme código abaixo:

```java
public class MinhaEntidade {
    
    @ManyToMany
    private Collection<Pessoa> donos = new ArrayList<>();

}
```

#### @OneToOne

Anotação utilizada para especificar um relacionamento de banco de dados um para um, conforme código abaixo:

```java
public class MinhaEntidade {
    
    @OneToOne
    private Montadora montadora;

}
```

Quer saber mais sobre as notações do JPA, acesso o [link!](https://dzone.com/articles/all-jpa-annotations-mapping-annotations)

## Como declarar meu repositório?

Antes de aprendermos a declarar nosso repositório, o que é o repositório no Spring Data?

#### O que é o repositório?

O repositório é uma classe que representa as operações do banco de dados da sua entidade, como por exemplo:

- Salvar
- Alterar
- Buscar
- Remover

#### Declarando nosso repositório

Já sabemos a responsabilidade do repositório, para declarar o mesmo o Spring Data fornece algumas interfaces:

**Repository**

Repository é uma interface de marcação, sem métodos, para que o Spring entenda que a classe é um repositório e faça todas as configurações 
necessárias.

Geralmente não é muito utilizada, pois precisamos declarar todas as nossas operações que gostaríamos.

Não seria legal termos já um repositório com todas as operações padrão?

Pensando nisso a comunidade do Spring criou a interface [CrudRepository](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html).

**CrudRepository**

Antes de falarmos sobre o CrudRepository, precisamos entender o que significa CRUD.

O CRUD é um acrônimo em inglês para as 4 operações básicas de um banco de dados:

- **C**reate: Representado pela operação insert.
- **R**ead: Representado pela operação select.
- **U**pdate: Representado pela operação update.
- **D**elete: Representado pela operação delete.

Agora que sabemos o significado de CRUD fica muito dedutível a interface CrudRepository, na qual representa essas operações:

- **save:** Salve ou atualiza uma entidade.
- **saveAll:** Salva ou atualiza um conjunto de entidade.
- **deleteById:** Remove uma determinada entidade, de acordo com sua identificação.
- **deleteAll:** Remove todas as entidades.
- **findById:** Busca uma determinada entidade, de acordo com sua identificação.
- **findAll:** Busca todas as entidades.

Quer sabemos mais sobre os métodos dessa interface, acesse o [link!](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html)

Não seria legal além de termos as operações de CRUD, termos a possibilidade ordenar e limitar nossas consultas?

Pensando nisso a comunidade do Spring criou a interface [PagingAndSortingRepository](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/PagingAndSortingRepository.html).

**PagingAndSortingRepository**

PagingAndSortingRepository é uma interface que herda a CrudRepository, ou seja, tem todos os métodos CRUD complementando 
os mesmo com a possibilidade de ordenar e ou limitar as consultas.

- **findAll(Pageable pageable):** Busca todas as entidades e aplica a ordenação e limite configurado passado como Pageable.
- **findAll(Sort sort):** Busca todas as entidades e aplica o(s) limite(s) configurado passado como Sort.

Para ordenar ou limitar as consultas é precisso passar o seguinte objeto:

- **Pageable**: Limita e pagina as consultas.
- **Sort**: Ordena as consultas.

Código de exemplo:

**Limitando \ Paginando**

```java
public class Example {

    public void someMethod() {
        Integer page = 1;
        Integer size = 1;
        PageRequest pageRequest = PageRequest.of(page, size);
        repository.findAll(pageRequest);
    }

}
```

**Ordenando**

```java
public class Example {

    public void someMethod() {
        Collection<String> fields = new ArrayList<>("nome");
        Sort sort =Sort.by(Sort.Direction.DESC, fields);
        repository.findAll(sort);
    }

}
```

**Paginando e Ordenando**

```java
public class Example {

    public void someMethod() {
        Collection<String> fields = new ArrayList<>("nome");
        Sort sort =Sort.by(Sort.Direction.DESC, fields);
        
        Integer page = 1;
        Integer size = 1;
        
        PageRequest pageRequest = PageRequest.of(page, size, sort);
        repository.findAll(pageRequest);
    }

}
```

Quer sabemos mais sobre os métodos dessa interface, acesse o [link!](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/PagingAndSortingRepository.html)

---

Já sabemos sobre as interfaces de repositório do Spring Data, como eu declaro?

Para declarar seu repositório é necessário algumas passos, conforme abaixo:

1º Precisamos ter nossa entidade declarada.

Não sei declarar minha entidade, não tem problema, nesta página existe um tutorial (Como mapear minha entidade?) 
para te auxiliar.

2º Após ter configurado sua entidade, precisamos criar um interface que vai representar o repositório da mesma, conforme 
código abaixo:

```java
public interface CarroRepository extends CrudRepository<Carro, String> {

}
```

No primeiro parâmetro da interface CrudRepository deve ser passado a sua entidade, e no segundo o tipo do identificador.

3º Precisamos dizer para o Spring que existe um repositório que necessita ser configurado pelo mesmo, para tal, devemos 
anotar nosso repositório com a anotação @Repository

```java
@Repository
public interface CarroRepository extends CrudRepository<Carro, String> {

}
```

Quer saber mais sobre a anotação @Repository, acesse o [link!](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.namespace)

Quer saber mais sobre os repositórios no Spring Data, acesse o [link!](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.definition-tuning)

Eba, temos nosso repositório criado e configurado!