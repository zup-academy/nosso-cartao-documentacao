# Externalizando mensagens em um projeto web com Spring Boot

Na nossa aplicação podem acontecer erros de validação de entrada de dados, principalmente na borda mais externa, ali no controller. Outras vezes também podem ser verificadas incosistências que também precisam ser avisadas para a aplicação cliente que está nos consumindo. Vamos olhar o código abaixo para materializarmos o que estamos falando.

```java
@RestController
public class AutoresController {
	
	@PersistenceContext
	private EntityManager manager;

	@PostMapping(value = "/autores")
	@Transactional
	public String cria(@RequestBody @Valid NovoAutorRequest request) {
		//1
		Autor autor = request.toModel();
		manager.persist(autor);
		return autor.toString();
	}

	
}

public class NovoAutorRequest {

	@NotBlank
	private String nome;
	@NotBlank
	@Email
	@UniqueValue(domainClass = Autor.class,fieldName = "email")
	private String email;
	@NotBlank
	@Size(max = 400)
	private String descricao;

	public NovoAutorRequest(@NotBlank String nome,
			@NotBlank @Email String email,
			@NotBlank @Size(max = 400) String descricao) {
		super();
		this.nome = nome;
		this.email = email;
		this.descricao = descricao;
	}
    
    //resto do código omitido
}
```
E se o nome, email ou descrição enviados pelo cliente não passarem pelas restrições, quais mensagens vão ser enviadas de volta? Neste momento simplesmente enviamos as mensagens padrões, estabelecidas dentro dentro da implementação da Bean Validation que estamos utilizando, que no caso é Hibernate Validator. 

## Usando a facilidade do Spring Boot para customizar mensagens

Para alterar cada uma das mensagens de validações numa aplicação utilizando Spring Boot, basta que seja criado um arquivo chamado ```messages.properties``` na raiz do classpath. Na estrutura padrão de projetos, isso ficaria em ```src/main/resources```, quando não estamos falando de código fonte. 

Com o arquivo criado, basta que a gente coloque as configurações necessárias. Segue um exemplo.

```
    NotBlank.novoAutorRequest.nome = Nome é obrigatório sim senhor(a)
    NotBlank.nome = Nome é obrigatório
    NotBlank = Campo obrigatório 
```

Na customização acima deixamos a progressão do nível mais específico de mensagem até o nível mais genérico. 

* No primeiro exemplo criamos uma mensagem customizada para o @NotBlank dentro da classe ```NovoAutorRequest``` para o atributo ```nome```. 
* No segundo exemplo dizemos que todo atributo ```nome``` anotado com @NotBlank vai ter aquela mensagem para a falha de validação. 
* No terceiro exemplo dizemos que qualquer atributo anotado com @NotBlank vai ter aquela mensagem quando falhar. 

## E quando falhar a conversão do parâmetro para o tipo do Java?

Além das falhas de validação por conta de valores que não obedeceram as restrições básicas, podem acontecer falhas de conversão básica entre parâmetros que vieram da requisição para o tipo que você declarou na sua classe. Alguns casos clássicos:

* O texto representando a data não veio no formato corret
* Um decimal veio separado por virgula em vez de vir separado por ponto. 

Quando este tipo de coisa acontecer, você também pode devoler mensagens customizadas. Basta que você utilize o mesmo ```messages.properties``` e acrescente entradas relativas a falhas de conversão.

```
typeMismatch.java.math.BigDecimal = O valor não é um decimal válido
typeMismatch.java.time.LocalDateTime = A data não veio formatada corretamente.
```

## Referenciando chaves em validações customizadas

Você também pode referênciar chaves do ```messages.properties``` em validações customizadas. Dá uma olhada no exemplo abaixo:

```java
@Override
	public void validate(Object target, Errors errors) {
		if (errors.hasErrors()) {
			return;
		}

		NovoAutorRequest request = (NovoAutorRequest) target;

		Optional<Autor> possivelAutor = autorRepository
				.findByEmail(request.getEmail());

		if (possivelAutor.isPresent()) {
            //novoAutorRequest.email.sendo-usado é a chave
			errors.rejectValue("email", "novoAutorRequest.email.sendo-usado",
					"Já existe um(a) outro(a) autor(a) com o mesmo email "
							+ request.getEmail());
		}
	}
```

O sistema de validação do Spring vai buscar o valor associado a chave ```novoAutorRequest.email.sendo-usado``` caso a validação customizada falhe (se você ainda não conhece de validação customizada pode ficar tranquilo(a)). Aí agora é só colocar essa entrada no arquivo ```messages.properties```. 

```
    NotBlank.novoAutorRequest.nome = Nome é obrigatório sim senhor(a)
    NotBlank.nome = Nome é obrigatório
    NotBlank = Campo obrigatório 
    novoAutorRequest.email.sendo-usado = O email deste autor já está sendo utilizado. 

```