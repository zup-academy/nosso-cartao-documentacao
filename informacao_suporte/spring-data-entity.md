# Como mapear minha entidade utilizando Spring Data?

Neste tutorial, iremos ver como mapear uma entidade utilizando o [Java Persistence API (JPA)](https://www.oracle.com/java/technologies/persistence-jsp.html).

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

# Informação de Suporte

Quer saber mais sobre as anotações do JPA? [clique aqui!](https://docs.oracle.com/javaee/7/api/javax/persistence/package-summary.html)