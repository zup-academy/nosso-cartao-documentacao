# Qual diferença do @Valid e @Validated?

Existem duas anotações para habilitar a validação da classe, parâmetro, etc.

Qual é a diferença entre elas?

A diferença é que na anotação [@Validated](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/validation/annotation/Validated.html) 
é possível utilizar a validação em grupo, já no Bean Validation é necessário utilizar a anotação [@GroupSequence](https://docs.oracle.com/javaee/7/api/javax/validation/GroupSequence.html).

Para usar a validação em grupo, precisamos definir uma interface de marcação, conforme código abaixo:

```java
public interface GrupoPrioridadeUm {}

public interface GrupoPrioridadeDois {}
```

Depois precisamos definir para cada validação \ restrição qual grupo ele pertence, conforme código abaixo:

```java
public class Pessoa {

    @NotNull(groups = { GrupoPrioridadeUm.class })
    @Positive(groups = { GrupoPrioridadeDois.class })
    private Integer idade;

}
```

E por último precisamos definir qual a ordem de execução dos grupos, conforme código abaixo:

```java
public class Exemplo {

    public void criarPessoa(@Validated({GrupoPrioridadeUm.class, GrupoPrioridadeDois.class}) Pessoa pessoa) {
        // Código omitido
    }

}
```