# Quais são os tipos de repositórios utilizados no Spring Data?

O Spring Data fornece três tipos de repositóriso, conforme abaixo:

## Repository

Repository é uma interface de marcação, sem métodos, para que o Spring entenda que a classe é um repositório e faça todas as configurações 
necessárias.

Geralmente não é muito utilizada, pois precisamos declarar todas as nossas operações que gostaríamos.

Não seria legal termos já um repositório com todas as operações padrão?

Pensando nisso a comunidade do Spring criou a interface [CrudRepository](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html).

## CrudRepository

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

Não seria legal além de termos as operações de CRUD, termos a possibilidade ordenar e limitar nossas consultas?

Pensando nisso a comunidade do Spring criou a interface [PagingAndSortingRepository](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/PagingAndSortingRepository.html).

## PagingAndSortingRepository

PagingAndSortingRepository é uma interface que herda a CrudRepository, ou seja, tem todos os métodos CRUD complementando 
os mesmo com a possibilidade de ordenar e ou limitar as consultas.

- **findAll(Pageable pageable):** Busca todas as entidades e aplica a ordenação e limite configurado passado como Pageable.
- **findAll(Sort sort):** Busca todas as entidades e aplica o(s) limite(s) configurado passado como Sort.

# Informação de Suporte

Quer saber mais sobre CrudRepository, acesse o [link!](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html)

Quer saber mais sobre PagingAndSortingRepository, acesse o [link!](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/PagingAndSortingRepository.html)