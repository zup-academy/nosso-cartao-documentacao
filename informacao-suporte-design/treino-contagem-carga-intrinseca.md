# Treino de contagem de contagem de carga intrínseca

Sempre que você acabar um fluxo de código, verifique a carga intrínseca de cada uma das classes e mantenha o limite estabelecido para nosso treinamento. Vou deixar aqui um lembrete para você :). 

* Classes com atributos de dependência devem ter no máximo 7 pontos de carga intrínseca. Aqui entram principalmente as classes anotadas com @Controller e com @Service. 
* Classes com atributo de estado devem ter no máximo 9 pontos de carga intrínseca. Aqui em geral vão entrar classes anotadas com @Entity, também classes que representam os dados de uma requisição, classes possivelmente anotadas com @Embeddable. 

A métrica derivada do CDD que estamos trabalhando é a seguinte:

* Acoplamento com classes específicas do sistema contam um 1 ponto. É o que chamamos de **acoplamento contextual**. Lembrando que o acoplamento só conta ponto uma vez. Se a mesma classe é referenciada mais de uma vez, continua contando só um ponto.
* Toda branch de código conta um ponto
    * if   
    * else
    * loops(for,while,do while)
    * switch
    * case
    * try
    * catch
    * ? do operador ternário
    * : do operador ternário
* Toda passagem de função como argumento utilizando a sintaxe do Java 8 conta ponto. 

## Exemplo de ponto para acoplamento contextual

```java
public class AutoresController {

	@PersistenceContext
	private EntityManager manager;
	@Autowired
    //1
	private ProibeEmailDuplicadoAutorValidator proibeEmailDuplicadoAutorValidator;

	@InitBinder
	public void init(WebDataBinder binder) {		
		binder.addValidators(proibeEmailDuplicadoAutorValidator);
	}

	@PostMapping(value = "/autores")
	@Transactional

    //1
	public String cria(@RequestBody @Valid NovoAutorRequest request) {
        //1
		Autor autor = request.toModel();
		manager.persist(autor);
		return autor.toString();
	}


}
```

As seguinte classes contaram pontos de acoplamento contextual:

* ProibeEmailDuplicadoAutorValidator
* NovoAutorRequest
* Autor

E por que ```EntityManager``` não contou ponto? Porque é uma interface que vem da JPA, ou seja algo externo que deveríamos saber no projeto. Claro que se JPA não for ok para você, isso vai dificultar seu entendimento. Por outro lado fica claro um ponto de melhoria que você deve correr atrás. 

## Exemplo para contagem de ponto de branch

```java
        //1
		if (assignedAdvisor == null) {
			throw new ValidationException(
					"Could not determine the Early Alert Advisor for student ID "
							+ student.getId());
		}
        //1
		if (student.getCoach() == null
				|| assignedAdvisor.equals(student.getCoach().getId())) {
			student.setCoach(personService.get(assignedAdvisor));
		}

		ensureValidAlertedOnPersonStateNoFail(student);

		// Create alert
		final EarlyAlert saved = getDao().save(earlyAlert);

		// Send e-mail to assigned advisor (coach)
        //1
		try {
			sendMessageToAdvisor(saved, earlyAlert.getEmailCC());
		} 
        //1
        catch (final SendFailedException e) {
			LOGGER.warn(
					"Could not send Early Alert message to advisor.",
					e);
			throw new ValidationException(
					"Early Alert notification e-mail could not be sent to advisor. Early Alert was NOT created.",
					e);
		}
```

Perceba que marquei com um cada branch de código encontrada. Essa contagem tende a ser bem direta. 

## Ponto para passagem de função como argumento

```java
    Collection<Autor> autores = autorRepository.findAll();
    //1
    autores.foreach(autor -> {
        System.out.println(autor);
    });

    //1
    autores.foreach(System.out :: println);
```

Acima foi utilizado duas formas de passagem de função como argumento suportada pelo java. São simplesmente duas formas de fazermos a mesma coisa, a segunda utiliza um recurso chamada *method reference*. Ambos os casos contam um ponto :). 

## Calculando a pontuação total

A nossa métrica é por classe. Então você sempre precisa calcular a pontuação total para a classe e aí verificar se passou do limite. Passou? Refatore e fique no limite. Vamos manter o controle da complexidade do nosso projeto!

