# Qual diferença do @Valid e @Validated

Existem duas anotações para habilitar a validação da classe, parâmetro, etc.

Qual é a diferença entre elas.

Bom a anotação [@Valid](https://docs.oracle.com/javaee/7/api/javax/validation/Valid.html) é padrão da especificação 
do [Bean Validation](https://docs.oracle.com/javaee/7/api/javax/validation/package-summary.html), porém a mesma não tem
uma determinada funcionalidade requerida pela comunidade.

Quando o mesmo atributo tem duas ou mais anotações, gostariamos de adicionar uma ordem de execução, porém isso não é possível.

Visando isto a comunidade do Spring criou a anotação [@Validated](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/validation/annotation/Validated.html) 
na qual criou o conceito de validações em grupo.

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

E por último precisamos definir qual a ordem de execução, gostaríamos de executar primeiro a verificação de nullo e depois 
a verificação se o número é positivo:

```java
public class Exemplo {

    public void criarPessoa(@Validated({GrupoPrioridadeUm.class, GrupoPrioridadeDois.class}) Pessoa pessoa) {
    // ...
    }

}
```