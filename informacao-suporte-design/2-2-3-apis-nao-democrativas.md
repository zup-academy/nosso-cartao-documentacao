# API's não democráticas

O pilar completo é este: **A sua api deve deixar claro o caminho que deve ser seguido pelo ponto do código que decide usá-la. Não espere que ninguém lembre de invocar nada. Faça de tudo para gerar obrigações. Quanto mais específico é seu código, menos democrático ele é.**

Aqui partimos do princípio que o código é um bicho mutante, que está em constante evolução e sendo mantido por pessoas diferentes ao longo do tempo.

No mundo ideal manter um código deveria ser tipo manter uma geladeira, um carro, um fogão ou algo do genêro. Todo mundo que entende do assunto é capaz de manter aquele produto sem muito estresse.

Só que a realidade é bem diferente. Enquanto uma geladeira tende a ter os componentes implementados do mesmo jeito depois de um certo tempo, um código, muitas vezes, nem tem mais aquele componente ou ele já mudou tanto que o conhecimento anterior passa sobre aquilo passa a ter menos peso. 

## O perigo da falta de estabilidade dos contratos

Vamos olhar para o seguinte exemplo de código. Tente prestar bastante atenção no uso do objeto do tipo ```Person```. 

```java
	public void ensureValidAlertedOnPersonStateOrFail(Person person)
			throws ObjectNotFoundException, ValidationException {
		
		if ( person.getObjectStatus() != ObjectStatus.ACTIVE ) {
			person.setObjectStatus(ObjectStatus.ACTIVE);
		}

		final ProgramStatus programStatus =  programStatusService.getActiveStatus();

		if ( programStatus == null ) {
			throw new ObjectNotFoundException(
					"Unable to find a ProgramStatus representing \"activeness\".",
					"ProgramStatus");
		}
		
		Set<PersonProgramStatus> programStatuses =
				person.getProgramStatuses();
		//1
		if ( programStatuses == null || programStatuses.isEmpty() ) {
			PersonProgramStatus personProgramStatus = new PersonProgramStatus();
            //codigo omitido
		}

		//1
		if ( person.getStudentType() == null ) {
            //codigo omitido
			person.setStudentType(studentType);
		}
        
```

O código acima usa 5 métodos públicos da classe ```Person```, mas ela tem mais de 70 métodos públicos! 

Enquanto que a classe ```Person``` é transversal ao sistema todo, este método é específico para um fluxo. Classes transversais e construídas dentro da própria aplicação tendem a sofrer mais alterações do que pontos específicos. 

Além disso da possibilidade de sofrer mais alterações, tem o fato do método ```ensureValidAlertedOnPersonStateOrFail``` pedir um argumento com mais de 70 métodos públicos enquanto ele só usa 5. Existe a chance do outro ponto do código estar carregando um objeto ```Person``` para a memória, com todos seus relacionamentos e tudo mais. 

Quando você for escrever um teste automatizado também vai precisar criar o objeto completo. 

A única forma do ponto de código que invoca este método não carregar o objeto completo seria se ele conhecesse a implementação. E se a implementação mudar? Você já sabe que software muda, então não parece uma decisão sensata achar que aquilo não vai mudar.

## Precisamos de interfaces específicas e estáveis

Uma outra versão, do mesmo código, poderia ser essa:

```java
	public void ensureValidAlertedOnPersonStateOrFail(PossibleValidAlertedPerson person)
			throws ObjectNotFoundException, ValidationException {
		
		if ( person.getObjectStatus() != ObjectStatus.ACTIVE ) {
			person.setObjectStatus(ObjectStatus.ACTIVE);
		}

		final ProgramStatus programStatus =  programStatusService.getActiveStatus();

		if ( programStatus == null ) {
			throw new ObjectNotFoundException(
					"Unable to find a ProgramStatus representing \"activeness\".",
					"ProgramStatus");
		}
		
		Set<PersonProgramStatus> programStatuses =
				person.getProgramStatuses();
		//1
		if ( programStatuses == null || programStatuses.isEmpty() ) {
			PersonProgramStatus personProgramStatus = new PersonProgramStatus();
            //codigo omitido
		}

		//1
		if ( person.getStudentType() == null ) {
            //codigo omitido
			person.setStudentType(studentType);
		}
        
```

Perceba que só foi modificado o tipo do argumento de entrada, o resto ficou igual. ```PossibleValidAlertedPerson``` pode ser uma interface com apenas os 5 métodos necessários para aquele método. O que ganhamos?

* O ponto de invocação sabe exatamente o que precisa ser passado;
* A interface é específica para o método e, consequentemente, mais estável;
* Escrever testes automatizados tende a ser mais fácil, já que agora você precisa montar algo muito menor;

Aqui é uma técnica de orientação objetos que ficou famosa através do *SOLID*. Usamos a letra *I* que é o princípio da segregação pela interface. A ideia é criar contratos específicos para métodos, fazendo a aposta que essa espeficidade vai gerar um contrato mais estável e manutenível no futuro. 

O ponto de atenção é que, pela métrica mais usada derivada do CDD, todo acoplamente específico conta ponto. Então você vai precisar usar a técnica com parcimônia. 