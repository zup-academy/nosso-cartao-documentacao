# Um objeto muitas representações

É mais do que normal numa aplicação web que o mesmo objeto de uma classe com atributos de dados seja representado de N formas diferentes em funcionalidades diferentes. Por exemplo, pensando num domínio de ecommerce de livros, temos duas situações básicas:

* Listagem de livros
* Detalhe de um livro

Temos duas funcionalidades diferentes construídas em cima de um mesmo objeto. Como fazer?

## E se o livro for o responsável por retornar suas representações?

Um primeiro pensamento, inclusive conectado com o conceito de deixar estado perto do comportamento, pode ser o de deixar tais métodos dentro da própria classe ```Livro```. 

```java
@Entity
public class Livro {
@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	private @NotBlank String titulo;
	private @NotBlank @Size(max = 500) String resumo;
	private @NotBlank String sumario;
	private @NotNull @Min(20) BigDecimal preco;
	private @Min(100) int numeroPaginas;
	private @NotBlank String isbn;
	@NotNull
	private @Future LocalDate dataPublicacao;
	@ManyToOne
	private @NotNull @Valid Autor autor;
	@ManyToOne
	private @NotNull @Valid Categoria categoria;

    //construtor

    public LivroListagemResponse toLivroListagemResponse(){
        return new LivroListagemResponse(this);

        //uma outra implementação era passar dado por dado. 
    }    

    public LivroDetalheResponse toLivroDetalheResponse(){
        return new LivroDetalheResponse(this);
        //uma outra implementação era passar dado por dado. 
    }        
}
```

O código num endpoint ficaria assim:

```java
    public List<LivroListagemResponse> todos(){
        return livroRepository.findAll().stream().map(livro -> {
            return livro.toLivroListagemResponse();
        });
    }
```

Você tem três pontos de atenção:

* Pelo olhar da métrica de complexidade derivada do CDD você está aumentando um ponto para cada referência dentro da classe Livro. Ou seja, está correndo o risco de sua classe estar aumentando a dificuldade de entendimento. 
* Você não diminui os pontos de complexidade do ponto de vista do controller, já que o retorno continua o mesmo.
* O número de métodos na classe ```Livro``` cresce exatamente igual ao número de representações dos objetos da classe. Justamente porque essa classe é transversal ao negócio, enquanto que a representação é específica. 

## E se o livro não for responsável por retornar suas representações?

Aqui é uma solução, utilizando as mesmas classes por sinal, só combinando de maneira diferente. A classe ```Livro``` não sofre nenhuma alteração em função das representações do Livro em si. 

```java
    public List<LivroListagemResponse> todos(){
        return livroRepository.findAll().stream().map(livro -> {
            return new LivroListagemResponse(livro);
        });
    }
```

Fazendo agora mesma análise.

* Pelo olhar da métrica de complexidade derivada do CDD a classe ```Livro``` continua exatamente igual.
* Você não diminui os pontos de complexidade do ponto de vista do controller, já que o retorno continua o mesmo. Ou seja aqui ficou igual a anterior.
* O número de métodos na classe ```Livro``` **não** cresce exatamente igual ao número de representações dos objetos da classe. Justamente porque essa classe é transversal ao negócio e a gente decidiu não acoplar o transversal com algo super específico e instável. 

## Olhar crítico sobre suas decisões

Perceba que tentamos aqui ter um olhar crítico sobre nossa decisão. Quanto menos sentimento e mais fundamento, melhor para todas as pessoas envolvidas na construção do código.