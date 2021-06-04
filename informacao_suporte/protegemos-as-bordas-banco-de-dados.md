# O banco de dados também é uma borda

De vez em quando nem parece, mas o banco de dados também é uma borda da aplicação. E estamos falando sobre uma borda externa onde esperamos que todos os dados estejam VÁLIDOS. Como você pode fazer para adicionar uma proteção extra por lá também?

## Constraints

Todo banco de dados relacional maduro suporta a adição de constraints em relação a sua coluna. Abaixo temos algumas das restrições que você pode adicionar. Os exemplos abaixo vem de fontes diferentes, algumas vezes Mysql e outras da w3schools, mas as restrições mais comuns são suportadas por todos os bancos famosos do mundo relacional.

* [Tamanho máximo da coluna;](https://dev.mysql.com/doc/refman/8.0/en/char.html)
* [Enums;](https://dev.mysql.com/doc/refman/8.0/en/enum.html)
* [Restrição de valores não nulos;](https://www.w3schools.com/sql/sql_notnull.asp)
* [Chaves estrangeiras](https://www.w3schools.com/sql/sql_foreignkey.asp)

## Imagine que toda borda interna desconhece a externa

Abaixo vamos ver um novo exemplo usando Java como linguagem. A ideia vale para as suas tabelas também.

Quando você está dentro de uma borda do sistema, por exemplo dentro de um método, não é incomum a gente ter o seguinte pensamento: "Este parâmetro foi validado do lado de fora, então não preciso validar aqui neste método".

```java
    public AlgumTipoDeObject buscaPorId(Long id){
        //logica aqui
    }
```
Olhando só para este método como você que o ```id``` não é nulo? Enquanto programamos nossos vieses nos acompanham o tempo todo. Ainda mais se você for o responsável pela criação do comportamento e também pela invocação do mesmo. 

A recomendação é que sempre que possível, verifique se os parâmetros de entrada respeitam o necessário para a execução correta do método. 

```java
    public AlgumTipoDeObject buscaPorId(Long id){
        if(id == null){
            throw new IllegalArgumentoException("o id para busca não pode ser nulo")
        }
        //logica aqui
    }
```

Se o id chegar nulo, você tem um bug, tal fluxo deveria ser interrompido e uma falha deveria ser gerada no sistema. A vantagem é que agora você tem uma falha, gerada por um bug que está mais fácil de rastrear, já que você se defendeu e colocou uma mensagem razoável para próxima pessoa. 

Você deve encarar suas tabelas do mesmo jeito. Você não sabe se quem disparou as operações relacionadas ao banco de dados realizou as validações corretas. Então não confie! Não confie em nenhum dado que chega de uma camada superior, eles sempre podem estar errados!



