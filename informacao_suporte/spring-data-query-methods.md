# Como fazer consultas no banco de dados?

Para fazer consultas no Spring Data é utilizado uma funcionalidade denominada Query Methods.

## Query Methods

Query methods é uma funcionalidade na qual você declara a operação no banco de dados de acordo com o nome do método, 
para isso é necessário seguir algumas regras.

Ops, não entendi, declarar uma operação de acordo com o nome do método?

É isso mesmo, fique calmo, vamos detalhar melhor!

Digamos que eu tenho o seguinte método no meu repositório:

```java
@Repository
public interface MeuRepositorio extends CrudRepository<MinhaEntidade, String> {

    MinhaEntidade findByNome(String nome);

}
```

Ao chamar o método `findByNome` você está executando esse SQL:

`SELECT * FROM MINHA_ENTIDADE WHERE NOME = <VALOR DO PARÂMETRO>;`

O Spring Data irá interpretar esse método e gerar a operação de acordo com o banco de dados, como tudo que é 
interpretado necessita de seguir algumas regras, e quais são elas?

Para efetuar uma busca seu método deve começar com `find` e em seguida você deve utilizar algumas das expressões abaixo:

|Palavra Chave|Exemplo|Consulta|
|---|---|---|
|And|findByLastnameAndFirstname|… where x.lastname = ?1 and x.firstname = ?2|
|Or|findByLastnameOrFirstname|… where x.lastname = ?1 or x.firstname = ?2|
|Is, Equals|findByFirstname,findByFirstnameIs,findByFirstnameEquals|… where x.firstname = ?1|

Esses são apenas alguns exemplos, se deseja ver todas as possibilidades, acesse o [link!](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation)

**Retornos**

Caso deseja retornar apenas um elemento na consulta, devemos declarar como retorno a Entidade, conforme código abaixo:

```java
@Repository
public interface MeuRepositorio extends CrudRepository<MinhaEntidade, String> {

    MinhaEntidade findByNome(String nome);

}
```

* Ponto de atenção, se a consulta retornar mais que um elemento o Spring irá gerar a exception [IncorrectResultSizeDataAccessException](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/dao/IncorrectResultSizeDataAccessException.html)

Caso deseja retornar uma lista de entidade, devemos declarar o retorno do tipo lista, conforme código abaixo:

```java
@Repository
public interface MeuRepositorio extends CrudRepository<MinhaEntidade, String> {

    Collection<MinhaEntidade> findBySexo(String sexo);

}
```

**Parâmetros**

Os parâmetros são ordenados de acordo com o declarado no método, ou segue a primeira cláusula irá utilizar o valor do 
primeiro parâmetro e assim sucessivamente, conforme exemplo abaixo:

```java
@Repository
public interface MeuRepositorio extends CrudRepository<MinhaEntidade, String> {

    Collection<MinhaEntidade> findBySexoAndCidade(String sexo, String cidade);

}

public class Exemplo {
    
    @Autowired
    private MeuRepositorio meuRepositorio;

    public void metodoDeExemplo() {
        String sexo = "Masculino";
        String cidade = "São Paulo";
       meuRepositorio.findBySexoAndCidade(sexo, cidade);
    }

}
```

## Informação de Suporte

Quer saber mais sobre os Query Methods? [clique aqui!](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods)
