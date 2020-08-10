## Cuidado no exagero no uso dos mocks

Aqui é um texto rápido que serve mais como alerta. Por mais que o uso de um projeto como o Mockito nos ajude muito, é super importante você manter na mente que o objetivo principal da sua suite de testes é o de revelar bugs no sistema. Isso vem antes de tudo.

Cada vez que você usa um recurso de imitação provido pelo Mockito o que você tenha implementado na mão você deixa seu teste mais longe de executar próximo da realidade que vai ser encontrada. Se ficar muito longe, você pode se perguntar: Será que meu teste está realmente tentando achar algum problema?

Utilize os mocks sempre pensando em minimizar a sua utilização, por mais contraditório que isso pareça. Olhe o seguinte exemplo composto por um trecho de código real e um teste automatizado.

```java
	public ResponseEntity<?> cria(
			@RequestBody @Valid ClasseRequest request,UriComponentsBuilder builder) {
		if(algumRepository.findByAtributo(request.getInformacao()).isPresent()) {
			throw new ResponseStatusException(HttpStatus.UNPROCESSABLE_ENTITY);
		}

		AlgumObjeto objeto = request.toModel();
		manager.persist(objeto);
		
		URI enderecoConsulta = builder.path("/propostas/{id}").build(novaProposta.getId());
		return ResponseEntity.created(enderecoConsulta).build();
	}
```

```java
	@Test
	@DisplayName("uma descrição linda escrita em lingua portuguesa")
	void teste1() {
		EntityManager manager = Mockito.mock(EntityManager.class);
        AlgumRepository algumRepository = Mockito.mock(AlgumRepository.class);
		ClasseDeFluxo classeDeFluxo = new ClasseDeFluxo(manager, algumRepository);
        //define a informação que vai ser buscada no fluxo do código
		ClasseRequest request = new ClasseRequest("123456789");
		UriComponentsBuilder builder = UriComponentsBuilder.newInstance();
		
        //imitacao
        Mockito.when(algumRepository.findByAtributo("123456789")).thenReturn(Optional.of("valor"));

		Assertions.assertThrows(ResponseStatusException.class, () -> {
			classeDeFluxo.cria(request, builder);			
		});
	}
```

No trecho de código exibido utilizamos o mockito, mas colocamos um valor real na definição da expectativa de funcionamento do comportamento. Este mesmo teste poderia ter sido escrito assim:

```java
	@Test
	@DisplayName("uma descrição linda escrita em lingua portuguesa")
	void teste1() {
		EntityManager manager = Mockito.mock(EntityManager.class);
        AlgumRepository algumRepository = Mockito.mock(AlgumRepository.class);
		ClasseDeFluxo classeDeFluxo = new ClasseDeFluxo(manager, algumRepository);
        //define a informação que vai ser buscada no fluxo do código
		ClasseRequest request = new ClasseRequest("123456789");
		UriComponentsBuilder builder = UriComponentsBuilder.newInstance();
		
        //imitacao
        Mockito.when(algumRepository.findByAtributo(Mockito.anyString())).thenReturn(Optional.of("valor"));

		Assertions.assertThrows(ResponseStatusException.class, () -> {
			classeDeFluxo.cria(request, builder);			
		});
	}
```

O método ```anyString``` do Mockito é o que chamamos de **matcher**. Você ensina o Mockito que ele só precisa verificar que uma ```String``` foi passada para o método ```findByAtributo```, pouco importa qual. Ou seja, se outro valor for passado ali como argumento em vez da informação do objeto da classe ```ClasseRequest``` o código pode continuar funcionando.

Voltamos a afirmar: Utilize os mocks com parcimônia! Minimize as imitações e só faça uso do que realmente é necessário.