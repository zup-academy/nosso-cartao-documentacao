# Toda indireção aumenta a complexidade

**Toda indireção aumenta a dificuldade de entendimento da aplicação como um todo, ela precisa merecer existir. Ou seja, precisa ajudar a distribuir a carga intrínseca pelo sistema.**

Aqui estamos falando do caminho que o seu código precisa percorrer para que determinado fluxo de negócio seja executado. Tal caminho, em algum momento, também vai precisar ser percorrido pela pessoa que está buscando o entendimento do código como um todo. 

## Um exemplo de código com quase nenhuma indireção

```java
    public class CadastraUsuarioController {
        public void cadastra(Map<String,String> request){
            String nome = request.get("nome");
            String idadeEmTexto = request.get("idade");
            String email = request.get("email");

            if(nome == null || nome.trim().equals("")){
                //retorna dizendo que nome é invalido
            }

            Integer idade = null;
            try{
                idade = Integer.parse(idadeEmTexto);
            } catch(ParseException exception){
                 //retorna dizendo que nome é invalido
            }

            // continua com validações
            try {
                driverDoBanco.execute("insert into ...");
            } catch(SQLException exception){
                //retorna erro 500 informando uma falha
            }
        }
    }
```

O código usa construções básicas da linguagem, sem nenhuma abstração específica do próprio sistema. Teoricamente, neste código acima, caso a pessoa tenha familiaridade com a linguagem, não tem nada de novo. Por que não fazemos assim? 

* Mesmo usando só coisa padrão, este código pode ficar com tanto if, try etc que pode dificultar a compreensão;
* Parte deste código é extremamente repetitivo entre funcionalidades, então queremos poupar tempo e usar algo pronto;
* A figura do usuário é importante para vários pontos da aplicação, então queremos constuir um tipo nosso para representá-lo e fazer referência em outros lugares;
* Por mais que o ```Map``` seja uma construção padrão da linguagem