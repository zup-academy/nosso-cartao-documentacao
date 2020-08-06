## A necessidade da conversão

Combinamos de nunca conectar objetos de domínio com a borda mais externa do sistema. Só que, por conta disso, muitas vezes, precisamos pegar os dados deste objeto que vive nas bordas do sistema para criar um objeto que representa um conceito do nosso negócio em si. Abaixo temos um exemplo de uma classe que representa os dados de entrada de um endpoint.

```java
public class NovaPropostaRequest {

	@Email
	@NotBlank
	private String email;
	@NotBlank
	private String nome;
	@NotBlank
	private String endereco;
	@NotNull
	@Positive
	private BigDecimal salario;
	@CpfCnpj
	@NotBlank
	private String documento;

	public NovaPropostaRequest(@Email @NotBlank String email,
			@NotBlank String nome, @NotBlank String endereco,
			@Positive BigDecimal salario, String documento) {
		super();
		this.email = email;
		this.nome = nome;
		this.endereco = endereco;
		this.salario = salario;
		this.documento = documento;
	}
```

Só que na outra ponta, temos esta classe que representa o conceito do negócio.

```java
Entity
public class Proposta {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	private @Email @NotBlank String email;
	private @NotBlank String nome;
	private @NotBlank String endereco;
	private @Positive BigDecimal salario;
	@CpfCnpj
	@NotBlank
	private String documento;

	public Proposta(@Email @NotBlank String email, @NotBlank String nome,
			@NotBlank String endereco, @Positive BigDecimal salario,
			@CpfCnpj String documento) {
				this.email = email;
				this.nome = nome;
				this.endereco = endereco;
				this.salario = salario;
				this.documento = documento;
		// TODO Auto-generated constructor stub
	}
```

Como sair de um objeto do primeiro tipo e sair para um objeto do segundo tipo? 

## Utilizando classes conversoras no padrão de mercado

Uma forma de fazer isso é realizando a conversão direto no ponto de recebimento do parâmetro que representa os dados da requisição. 

```java
	public ResponseEntity<?> cria(
			@RequestBody @Valid NovaPropostaRequest request,UriComponentsBuilder builder) {

		Proposta novaProposta = new Proposta(request.getDocumento(),request.getEmail()...)
		manager.persist(novaProposta);
		
		URI enderecoConsulta = builder.path("/propostas/{id}").build(novaProposta.getId());
		return ResponseEntity.created(enderecoConsulta).build();
	}
```

Este código funciona e, para ser sincero, não tem problemas do ponto de vista de complexidade seguindo a nossa ideia de Cognitive Driven Development. Por outro lado, o mercado convencionou que este tipo de código não fica direto no controller. Então você vai um código mais ou menos assim:

```java
    
    @Autowired
    private NovaPropostaRequestToPropostaConverter novaPropostaRequestToPropostaConverter;
	public ResponseEntity<?> cria(
			@RequestBody @Valid NovaPropostaRequest request,UriComponentsBuilder builder) {

		Proposta novaProposta = novaPropostaRequestToPropostaConverter.converte(request);
		manager.persist(novaProposta);
		
		URI enderecoConsulta = builder.path("/propostas/{id}").build(novaProposta.getId());
		return ResponseEntity.created(enderecoConsulta).build();
	}
```

Inclusive existem projetos utilizados na Zup como o [Map Struct](https://mapstruct.org/) que automatizam este tipo de código. 

## Request Value Objects (classes de request inteligentes)

Agora, inspirado pela nossa ideia de Cognitive Driven Development, entendemos que classes que possuem atributos de dados podem ter comportamentos sobre estes atributos perto delas, desde que o limite de complexidade seja respeitado. Dito isso, uma outra ideia de fazer o mesmo código é a seguinte:

```java
	public ResponseEntity<?> cria(
			@RequestBody @Valid NovaPropostaRequest request,UriComponentsBuilder builder) {

		Proposta novaProposta = request.toModel();
		manager.persist(novaProposta);
		
		URI enderecoConsulta = builder.path("/propostas/{id}").build(novaProposta.getId());
		return ResponseEntity.created(enderecoConsulta).build();
	}
```

Perceba que a própria classe ```NovaPropostaRequest``` possui o comportamento para criar uma nova ```Proposta```.

```java
public class NovaPropostaRequest {

	@Email
	@NotBlank
	private String email;
	@NotBlank
	private String nome;
	@NotBlank
	private String endereco;
	@NotNull
	@Positive
	private BigDecimal salario;
	@CpfCnpj
	@NotBlank
	private String documento;

	public NovaPropostaRequest(@Email @NotBlank String email,
			@NotBlank String nome, @NotBlank String endereco,
			@Positive BigDecimal salario, String documento) {
		super();
		this.email = email;
		this.nome = nome;
		this.endereco = endereco;
		this.salario = salario;
		this.documento = documento;
	}

	public Proposta toModel() {
		return new Proposta(email,nome,endereco,salario,documento);
	}

}
```
Sugerimos que você utilize esta ideia durante as conversões de objetos de entrada(request) para objetos de domínio(representam o conceito). Entretanto precisamos que você fique alerta quando se deparar com outras formas de fazer o mesmo código. 