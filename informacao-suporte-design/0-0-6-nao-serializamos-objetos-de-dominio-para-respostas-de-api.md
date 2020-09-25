# Não serializamos objetos de domínio para respostas de API

Essa daqui é uma prática simples de ser seguida e que tende a facilitar a manutenção dos contratos da sua api. Imagine que você precisa retornar uma lista de livros como JSON a partir de um endpoint. Abaixo temos um possível código.

```java
    public List<Livro> todos(){
        return livroRepository.findAll();
    }

    public class Livro{
        private String nome;
        private BigDecimal preco;
        private Autor autor;
        private Categoria categoria;
        
        //getters para expor o que precisa ser exposto
    }
```

Não existe dúvida que esse código funciona. 

## A fragilidade do acoplamento

Por mais que do ponto de simplicidade o código esteja ótimo do ponto de vista do CDD, temos uma armadilha. 

* E se você adicionar mais um getter na classe Livro?
* E se você remover um getter da classe Livro?
* E se você criar um getQualquerCoisa?

Qualquer uma das modificações acima vai modificar a resposta final gerada por aquele endpoint. E ela é muito possível de acontecer, justamente porque ```Livro``` é uma classe que faz parte do núcleo da aplicação e tem mais chances de sofrer modificações que cruzem a aplicação inteira. 

## Criando uma representação para o endpoint

Uma solução que adiciona um ponto de complexidde, dado a métrica que estamos trabalhando derivada do CDD, mas que diminui a fragilidade do contrato é a de criar uma classe específica para a saída de determinado endpoint. 

```java
    public List<LivroListagemResponse> todos(){
        return livroRepository.findAll().stream().map(livro -> {
            return new LivroListagemResponse(livro);
        });
    }

    public class LivroListagemResponse {
        private String nome;
        private BigDecimal preco;

        public LivroListagemResponse(Livro livro){
            this.nome = livro.getNome();
            this.preco = livro.getPreco();
        }
    }

    public class Livro{
        private String nome;
        private BigDecimal preco;
        private Autor autor;
        private Categoria categoria;
        
        //getters para expor o que precisa ser exposto
    }
```

Perceba que agora a classe ```LivroListagemResponse``` funciona como uma representante(Proxy) do livro para aquele endpoint. Vamos fazer as mesmas perguntas agora:

* E se você adicionar mais um getter na classe Livro?
* E se você remover um getter da classe Livro?
* E se você criar um getQualquerCoisa?

Para a primeira e terceira nada vai acontecer na nossa classe de saída. Já para a segunda vamos ter um erro de compilação, o que é ideal dentro de uma linguagem compilada. Mesmo se a linguagem for dinâmica, vamos tomar um erro em tempo de execução. 

Importante ressaltar que antes aquele trecho de código tinha dois pontos de complexidade e passou a ter três, por conta da referência a nova classe.