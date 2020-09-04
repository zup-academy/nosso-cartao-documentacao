# Como declarar meu repositório utilizando Spring Data?

Para declarar seu repositório é necessário algumas passos, conforme abaixo:

1º Precisamos ter nossa entidade declarada, não sabe como? [Aqui você encontra como fazer isso !!!](../informacao_suporte/spring-data-entity.md)

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

Eba, temos nosso repositório criado e configurado!

Você sabia que existem outros tipos de repositórios? Quer saber mais? Acesse o [link!](../informacao_suporte/spring-data-repository-types.md)

# Informação de Suporte

Quer saber mais sobre a anotação @Repository, acesse o [link!](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.namespace)

Quer saber mais sobre os repositórios no Spring Data, acesse o [link!](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.definition-tuning)