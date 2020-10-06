# Toda indireção aumenta a complexidade

**Toda indireção aumenta a dificuldade de entendimento da aplicação como um todo, ela precisa merecer existir. Ou seja, precisa ajudar a distribuir a carga intrínseca pelo sistema.**

Aqui estamos falando do caminho que o seu código precisa percorrer para que determinado fluxo de negócio seja executado. Tal caminho, em algum momento, também vai precisar ser percorrido pela pessoa que está buscando o entendimento do código como um todo. 

## Um exemplo de código com quase nenhuma indireção

```java
    public class CadastraUsuarioController {
    
        public void cadastra(Map<String,String> request) {
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
                PreparedStatement insert = driverDoBanco.prepareStatement("insert into Usuario(...) values(?,?,?)");
                insert.setString(1,nome);
                insert.setString(2,idade);
                insert.setString(3,email);
            } catch(SQLException exception){
                //retorna erro 500 informando uma falha
            }
        }
    }
```

O código usa construções básicas da linguagem, sem nenhuma abstração específica do próprio sistema. Teoricamente, neste código acima, caso a pessoa tenha familiaridade com a linguagem, não tem nada de novo. Por que não fazemos assim?

* Mesmo usando só coisa padrão, este código pode ficar com tantos `if`, `try` etc que pode dificultar a compreensão;
* Parte deste código é extremamente repetitivo entre funcionalidades, então queremos poupar tempo e usar algo pronto;
* A figura do usuário é importante para vários pontos da aplicação, então queremos constuir um tipo nosso para representá-lo e fazer referência em outros lugares;
* Por mais que o `Map` seja uma construção padrão da linguagem, a não ser que você tenha poderes mágicos, você não consegue saber as informações que ele tem lá dentro;

## Começamos a jornada das indireções

```java
    public class CadastraUsuarioController {
    
        public void cadastra(NovoUsuarioRequest request) {            
            if (!request.taValido()) {
                //retorna tudo que foi falha de validacao
            }
            
            try {
                PreparedStatement insert = driverDoBanco.prepareStatement("insert into Usuario(...) values(?,?,?)");
                insert.setString(1,request.getNome());
                insert.setString(2,request.getIdade());
                insert.setString(3,request.getEmail());
            } catch(SQLException exception) {
                //retorna erro 500 informando uma falha
            }
        }
    }

    public class NovoUsuarioRequest {
        private String nome;
        private String email;
        private int idade;

        //métodos necessários

        public boolean taValido() {
            //verificacao aqui
        }
    }
```

Adicionamos a classe `NovoUsuarioRequest` para que o framework em questão consiga já fazer a conversão dos parâmetros que vieram na requisição para um tipo específico da aplicação. 

Acabamos de colocar nossa primeira indireção e aumentamos a complexidade do sistema como um todo. A contrapartida é que diminuimos a complexidade deste ponto específico do código. Lembrando que aqui estamos sempre guiados(as) pela complexidade do ponto de vista cognitivo, sugerido pelo CDD. 

Só que ainda temos uma abstração nossa para representar os dados da requisição, onde está a abstração para representar o usuário transversal ao sistema?

## A indireção para o tipo considerado de domínio

```java
    public class CadastraUsuarioController {
    
        public void cadastra(NovoUsuarioRequest request) {            
            if (!request.taValido()) {
                //retorna tudo que foi falha de validacao
            }
            
            Usuario novoUsuario = request.paraUsuario();
            try {
                PreparedStatement insert = driverDoBanco.prepareStatement("insert into Usuario(...) values(?,?,?)");
                insert.setString(1,novoUsuario.getNome());
                insert.setString(2,novoUsuario.getIdade());
                insert.setString(3,novoUsuario.getEmail());
            } catch(SQLException exception) {
                //retorna erro 500 informando uma falha
            }
        }
    }

    public class NovoUsuarioRequest {
        private String nome;
        private String email;
        private int idade;

        //métodos necessários

        public boolean taValido() {
            //verificacao aqui
        }
        
        public Usuario paraUsuario() {
            //cria instância de Usuario a partir dos dados da request
        }
    }

    public class Usuario {
        private String nome;
        private String email;
        private int idade;

        //o que for necessário

    }
```

Agora temos mais uma indireção e a complexidade só aumenta :). Você pode até se perguntar, mas por qual motivo não recebemos o usuário direto ali? Lembre que [**não ligamos parâmetros de entrada de dados com o objetos de domínio**](https://github.com/claudiooliveirazup/documentacao-cartao-branco/blob/master/informacao-suporte-design/0-0-5-isolamos-parametros-do-dominio.md) pelos motivos já explicados no tópico referente a este pilar. 

Especificamente neste caso não ganhmos nada em troca, apenas a indireção a mais. Ou seja, o código ficou apenas mais complexo na esperança que isso possa ser positivo para o sistema como um todo. 

## A indireção para persistir objetos

```java
    public class CadastraUsuarioController {
    
        public void cadastra(NovoUsuarioRequest request) {            
            if (!request.taValido()) {
                //retorna tudo que foi falha de validacao
            }

            Usuario novoUsuario = request.paraUsuario();
            orm.persist(novoUsuario);
        }
    }

    public class NovoUsuarioRequest {
        private String nome;
        private String email;
        private int idade;

        //métodos necessários

        public boolean taValido() {
            //verificacao aqui
        }
        
        public Usuario paraUsuario() {
            //cria instância de Usuario a partir dos dados da request
        }
    }

    public class Usuario {
        private String nome;
        private String email;
        private int idade;

        //o que for necessário

    }
```

Finalmente chegamos agora na última indireção desse fluxo. Queremos nos livrar do código necessário para trabalhar com seu banco de dados. Aumentamos mais um pouco a complexidade do sistema como um todo, mas aí ganhamos na diminuição da complexidade deste ponto específico de novo. Dado que não temos mais tratamento de exceptions. 

## Código mais enxuto é menos complexo?

Perceba que no final você tem um código com menos linhas. Ele é necessariamente menos complexo? Como comentamos, você pode encarar complexidade como a teia de necessidades que você precisa dominar para entender determinado material, nesse caso um pedaço de código. 

No nosso exemplo final você tem algumas necessidades de entendimento:

* A classe `NovoUsuarioRequest`;
* A classe `Usuario`;
* A possível classe `ORM`;

Nada disso é padrão da linguagem. Duas são específicas do seu sistema e outra possivelmente é de um framework que pode ser utilizado em muitas aplicações diferentes. Ou seja, você precisa de outros entendimentos para que aquele pedaço de código fique realmente mais fácil. 

## Analisando o código pela métrica derivada do CDD 

Dada a métrica atual sugerida pelo CDD, entendemos que aquele código fica sim mais fácil. Justamente porque você deveria saber a priori sobre o ORM escolhido e, quando você faz a troca dos `ifs` e `trys` que estavam lá pelas indireções, o saldo fica positivo. Tudo vai depender da sua métrica de complexidade e do limite que você definiu. 

Só para deixar claro, você pode ter um código enxuto e com várias construções que sejam penalizadas pela métrica atual do CDD. Lembre que agora você tem um jeito sistemático de analisar complexidade e completamente factível por qualquer pessoa, use!

## Existe um limite de indireções?

A resposta para isso é não :). Não temos um limite de indireções, o que você precisa ter é clareza da troca que está fazendo. O código abaixo por exemplo:

```java
    public class CadastraUsuarioController {
    
        public void cadastra(NovoUsuarioRequest request) {            
            if (!request.taValido()) {
                //retorna tudo que foi falha de validacao
            }

            Usuario novoUsuario = request.paraUsuario();
            serviceNovoUsuario.cria(novoUsuario);            
        }
    }

    public class ServiceNovoUsuario {
        public void cria(Usuario novoUsuario)c{
            orm.persist(novoUsuario);
        }
    }

    public class NovoUsuarioRequest {
        private String nome;
        private String email;
        private int idade;

        //métodos necessários

        public boolean taValido()c{
            //verificacao aqui
        }
        
        public Usuario paraUsuario() {
            //cria instância de Usuario a partir dos dados da request
        }
    }

    public class Usuario {
        private String nome;
        private String email;
        private int idade;

        //o que for necessário

    }
```

Perceba que mais uma indireção foi criada e a complexidade do sistema como um todo aumentou, assim como a complexidade daquela unidade de código em específico. Isolando a análise em complexidade, só aumentou. O que você espera ganhar então? 

O mercado vai dizer que você esperar ganhar flexibilidade para a troca do mecanismo de persistência. E é verdade! Acha que precisa, jogue duro e vá por este caminho. Tendo clareza do que está sendo feito, tudo é liberado.

Uma pergunta que você pode se fazer é? Será que seria tão complicado trocar os pontos de erro de compilação que vão aparecer por conta da troca do mecanismo de persistência? 

## Recado final sobre indireção

Realmente toda indireção aumenta complexidade. Quanto mais unidades você precisa entender, mais complexo é aquele ecossistema. Por outro lado ninguém busca entender o código de um sistema de uma vez só, geralmente caminhamos por unidades de código que se relacionam para completar alguma atividade. Até onde vai a caminhada, depende muito da necessidade que você tem de entendimento do contexto naquele momento.

A sugestão é que você sempre faça a conta da complexidade cognitiva respeitando o limite combinado pela equipe em função da métrica derivada do CDD que foi escolhida. 
