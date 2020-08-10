# O que são Mocks?

Muitas vezes seu código depende de um comportamento que não é trivial de ser reproduzido, alguns exemplos:

* Realizar uma consulta em uma ou mais tabelas do banco de dados;
* Construir um objeto que depende de muitos parâmetros;
* Realizar a invocação de um método que necessita de um certo fluxo anterior para que ele produza o resultado esperado;

Vamos pegar o exemplo de acessar os dados gravados no banco de dados, porque ele nos empurra para utilizar um ```EntityManager``` direto ou um ```Repository``` da Spring Data JPA. Imagine que você tem um fluxo de código parecido com o seguinte:

```java
@RestController
public class ClasseDeFluxo {
	
	private EntityManager manager;
	private AlgumRepository algumRepository;
	
	
	
	public ClasseDeFluxo(EntityManager manager,
			AlgumRepository algumRepository) {
		super();
		this.manager = manager;
		this.algumRepository = bloqueiaDocumentoIgualValidator;
	}


	@PostMapping(value = "/propostas")
	@Transactional
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

}
```
O normal para o código acima é que a gente crie dois testes: Um que entre no if e outro que não. Só que temos algumas dificuldades:

* Como vamos fazer para executar o findByAtributo?
* Como vamos fazer para executar o persist?
* Será que existe alguma forma fácil de construirmos um UriComponentsBuilder na mão?

## Um esboço de como seria o código de teste

```java
	@Test
	@DisplayName("uma descrição linda escrita em lingua portuguesa")
	void teste1() {
		EntityManager manager = //criar um EntityManager
        AlgumRepository algumRepository = // criar um repository
		ClasseDeFluxo classeDeFluxo = new ClasseDeFluxo(manager, algumRepository);
		ClasseRequest request = new ClasseRequest(...);
		UriComponentsBuilder builder = UriComponentsBuilder.newInstance();
		
		Assertions.assertThrows(ResponseStatusException.class, () -> {
			classeDeFluxo.cria(request, builder);			
		});
	}
```

## Uma primeira alternativa para criar as dependências

Tanto ```EntityManager``` quanto ```AlgumRepository``` são interfaces. Então você poderia fazer o básico aqui que é criar implementações *fakes* dessas interfaces. O método ```cria``` não depende da implementação dessas interfaces e sim dos métodos públicos que estão expostos no contrato de utilização. 

```java
public class FakeEntityManager implements EntityManager{
    //todos os métodos aqui
}
```

```java
public class FakeAlgumRepository implements AlgumRepository {
    //todos os métodos aqui
}
```
Agora o código para execução do teste ficaria parecido com o que segue abaixo.

```java
	@Test
	@DisplayName("uma descrição linda escrita em lingua portuguesa")
	void teste1() {
		EntityManager manager = new FakeEntityManager();
        AlgumRepository algumRepository = new FakeAlgumRepository();
		ClasseDeFluxo classeDeFluxo = new ClasseDeFluxo(manager, algumRepository);
		ClasseRequest request = new ClasseRequest(...);
		UriComponentsBuilder builder = UriComponentsBuilder.newInstance();
		
		Assertions.assertThrows(ResponseStatusException.class, () -> {
			classeDeFluxo.cria(request, builder);			
		});
	}
```

Nas suas implementações fakes você pode deixar as implementações que bem entender para que o teste passasse pelo caminho esperado. Por exemplo você fazer com que o método ```findByAtributo``` retorne uma ```Optional``` vazia. Para o outro teste você pode fazer com que o método na classe *fake* retorne uma ```Optional``` preenchida. Especificamente sobre o ```FakeEntityManager``` você pode ter uma variável de controle que verifica a chamada do método ```save```. 

A ideia é que você consiga criar as **imitações** dos comportamentos esperados para que eles possam ser utilizados durante os testes. Dessa forma você isola mais a execução do teste. Por outro lado, diminui as chances de saber se aquele código realmente funciona quando tudo tiver sendo usado junto(integrado), é um tradeoff regular. 

## O problema de implementar os próprios imitadores

Muitas as vezes as interfaces vão ter muitos métodos e naquele ponto do código você só quer utilizar um determinado conjunto deles. Ainda mais quando a interface ou classe não está sob seu controle e sim sob o controle de um framework ou uma biblioteca, como é o caso do ```EntityManager```. 

Para este tipo de situação é que podemos fazer uso de bibliotecas que automatizam a criação destes imitadores, também conhecidos como **Mocks**! 

## Mockito para facilitar a criação de Mocks


Agora o código para execução do teste ficaria parecido com o que segue abaixo.

```java
	@Test
	@DisplayName("uma descrição linda escrita em lingua portuguesa")
	void teste1() {
		EntityManager manager = Mockito.mock(EntityManager.class);
        AlgumRepository algumRepository = Mockito.mock(AlgumRepository.class);
		ClasseDeFluxo classeDeFluxo = new ClasseDeFluxo(manager, algumRepository);
		ClasseRequest request = new ClasseRequest(...);
		UriComponentsBuilder builder = UriComponentsBuilder.newInstance();
		

		Assertions.assertThrows(ResponseStatusException.class, () -> {
			classeDeFluxo.cria(request, builder);			
		});
	}
```

Quando criamos um projeto com Spring Boot e optamos por utilizar o starter relativo a testes, já ganhamos o Mockito importado no nosso projeto. Basicamente o método ```mock``` serve para você criar uma implementação daquela classe/interface e começar a construir as imitações de comportamento. 

Agora vamos adicionar uma imitação de comportamento relativa a classe ```AlgumRepository```. 

```java
	@Test
	@DisplayName("uma descrição linda escrita em lingua portuguesa")
	void teste1() {
		EntityManager manager = Mockito.mock(EntityManager.class);
        AlgumRepository algumRepository = Mockito.mock(AlgumRepository.class);
		ClasseDeFluxo classeDeFluxo = new ClasseDeFluxo(manager, algumRepository);
		ClasseRequest request = new ClasseRequest(...);
		UriComponentsBuilder builder = UriComponentsBuilder.newInstance();
		
        //imitacao
        Mockito.when(algumRepository.findByAtributo(algumValorAqui)).thenReturn(Optional.of("valor"));

		Assertions.assertThrows(ResponseStatusException.class, () -> {
			classeDeFluxo.cria(request, builder);			
		});
	}
```

Agora quando o método ```findByAtributo```for invocado no fluxo do código, o retorno dele vai ser uma ```Optional``` preenchida. Por conta disso, o método ```isPresent``` vai retorna ```true`` e vamos cair no lançamento da exception esperada. 

Para saber sobre mais as possibilidades de uso do ```Mockito``` consulte a documentação oficial. 

## informação de suporte

O Mockito faz uso forte de uma funcionalidade da linguagem Java que é chamada de Proxy dinâmico. Tal funcionalidade é super utilizada em frameworks importantes como Spring e Hibernate. [Recomendamos que você busque mais informações sobre isso.](https://docs.oracle.com/javase/8/docs/technotes/guides/reflection/proxy.html) 

Também busque sobre projetos que facilitam a implementam de proxies dinâmicos através de geração de bytecode em tempo de execução. [O cglib é um dos mais famosos.](https://github.com/cglib/cglib). Assim como o [bytebuddy](https://bytebuddy.net/#/). 
