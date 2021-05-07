## Uma ideia para escopar transação com o banco de dados no Spring

```java
@Component
public class ExecutorTransacao {

	@PersistenceContext
	private EntityManager manager;
	
	@Transactional
	public <T> T salvaEComita(T objeto) {
		manager.persist(objeto);
		return objeto;
	}

	@Transactional
	public <T> T atualizaEComita(T objeto) {
		return manager.merge(objeto);
    }
    
    @Transactional
    public <T> T executa(Supplier<T> algumCodigoComRetorno){
        return algumCodigoComRetorno.get();
    }
}
```

A classe acima salva, atualiza e executa funções no escopo de uma transação. Ela tem uma complexidade baixa do ponto de vista tecnologias utilizadas(usa apenas o que é padrão do framework e da linguagem Java). De quebra ela pode ser reutilizada por todo santo projeto. 

## Exemplos de uso

```java
    @PostMapping(value = "/endereco")    
	public ResponseEntity<?> cria(@RequestBody AlgumRequest request) {
        AlgumModel model = request.toModel();
        executorTranscao.salvaEComita(model);

        AlgumResultado algumResultado = sistemaExterno.consultaViaHttp(model.getInformacao());
        
        model.atualiza(algumResultadoTransformado);
        executorTranscao.atualizaEComita(model);
	}
```

Uma outra possibilidade de uso, agora usando o método que espera um ```Supplier``` como argumento. 

```java
    @PostMapping(value = "/endereco")    
	public ResponseEntity<?> cria(@RequestBody AlgumRequest request) {
        AlgumModel model = request.toModel();
        executorTransacao.salvaEComita(model);

        AlgumResultado algumResultado = sistemaExterno.consultaViaHttp(model.getInformacao());
        
        AlgumModel modelAtualizado = executorTransacao.executa(() -> {
            model.atualiza(algumResultadoTransformado);
            return model;
        });
	}
```
