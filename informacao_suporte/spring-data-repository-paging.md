# Como paginar ou limitar consultas utilizando Spring Data?

Para paginar ou limiar as consultas do banco de dados a comunidade do Spring criou a interface [PagingAndSortingRepository](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/PagingAndSortingRepository.html).

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

# Informação de Suporte

Quer saber mais sobre os métodos dessa interface, acesse o [link!](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/PagingAndSortingRepository.html)