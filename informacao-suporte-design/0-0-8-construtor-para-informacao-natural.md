# Usamos o construtor para criar o objeto no estado válido.

Em vários momentos do seu código você vai precisa instanciar um objeto. Geralmente isso vai acontecer no momento de criação dos seus objetos que têm atributos de estado e que tais estados vão ser persistidos num banco de dados por exemplo. Abaixo segue um fluxo de criação de um autor para um ecommerce de livros, por exemplo. 

```java
public class NovoAutorRequest {

	@NotBlank
	private String nome;
	@NotBlank
	@Email
	private String email;
	@NotBlank
	@Size(max = 400)
	private String descricao;

    //construtor para receber os dados

	public Autor toModel() {
        //ponto de criação de um autor em função de informações da request
		return new Autor(this.nome,this.email,this.descricao);
	}
}
```

Dado que as informações de nome, email e descrição são obrigatórias, forçamos ela através do construtor definido na classe. 

```java
    public Autor(String nome, String email,String descricao) {
		this.nome = nome;
		this.email = email;
		this.descricao = descricao;
	}
```

Isto é suportado pelas linguagens e deve ser usado. Você deve forçar o máximo de caminhos dentro do seu código. 

## E o id, não vem pelo construtor?

A pergunta que você deve se fazer é: O id é obrigatório na construção do objeto?

Sempre que você usar um id auto gerado pelo seu banco de dados ele não vai ser obrigatório pelo construtor. Informação obrigatória pelo construtor é aquela que é natural. 

O id presente como atributo da sua classe só está lá por conta do banco de dados, no momento da criação do objeto você ainda não tem. 


## E por que eu não vou usar os métodos de acesso?

Você já deve ter visto o mesmo fluxo acima escrito da seguinte forma:

```java
	public Autor toModel() {
        //ponto de criação de um autor em função de informações da request
        Autor autor = new Autor();
        autor.setNome(this.nome);
        autor.setEmail(this.email);
        autor.setDescricao(this.descricao);
		return autor;
	}

```

E aí, lá na classe ```Autor``` está mais ou menos assim:

```java
    @Entity
    public class Autor {

        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;
        private @NotBlank String nome;
        private @NotBlank @Email String email;
        private @NotBlank @Size(max = 400) String descricao;        
        
        public Autor() {

        }

        //getters e setters
```

Este código indica que nenhuma informação do autor é obrigatória na construção do objeto. A pessoa precisa navegar na classe, olhar as annotations e aí chamar os métodos corretos. Se você pode escrever um código que vai guiar a pessoa para fazer o que você quer, por que vai fazer um que não vai guiar?

Só crie métodos de acesso quando eles forem realmente necessários. 

## Só que o framework precisa de um construtor sem argumentos

Existem alguns frameworks como Hibernate que podem exigir que você tenha um construtor sem argumentos. E claro, a gente não precisa deixar de usar um facilitador deste tamanho só porque não queremos colocar um construtor sem argumentos. Olha o que você pode fazer:

```java
    @Deprecated
	public Autor() {

	}

	public Autor(String nome, String email,
			String descricao) {
		this.nome = nome;
		this.email = email;
		this.descricao = descricao;
	}
```

Você pode deixar uma dica informando que o construtor sem argumentos é depreciado. Isso envia um sinal de alerta para a pessoa que pensar em chamá-lo. Você pode inclusive acrescentar um comentário com a explicação. 

Para você não ter que ficar escrevendo este construtor o tempo todo e colocando ```@Deprecated``` em cima, você pode também criar um atalho na sua ide. 