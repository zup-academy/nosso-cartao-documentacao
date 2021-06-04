## Ponto de atenção na hora demarcar a transação 

Uma forma muito direta de você demarcar uma transação no Spring é anotando um determinado método com a annotation ```@Transactional```. 

```java
    @PostMapping(value = "/endereco")
    @Transacional
	public ResponseEntity<?> cria(...) {
        //suposta implementacao aqui
	}
```

Caso você tenha apenas código que rodam em memória e eventualmente algum estado precise ser salvo no banco de dados, não tem perigo nenhum. Exemplo:

```java
    @PostMapping(value = "/endereco")
    @Transacional
	public ResponseEntity<?> cria(@RequestBody AlgumRequest request) {
        AlgumModel model = request.toModel();
        manager.persist(model);
	}
```

Agora, e se você tiver uma consulta a um sistema externo para consultar ou gerar alguma coisa?

```java
    @PostMapping(value = "/endereco")
    @Transacional
	public ResponseEntity<?> cria(@RequestBody AlgumRequest request) {
        AlgumModel model = request.toModel();
        manager.persist(model);

        AlgumResultado algumResultado = sistemaExterno.consultaViaHttp(model.getInformacao());
        //transfroma esse algumResultado
        model.atualiza(algumResultadoTransformado);
	}
```

No código acima seguramos uma transação enquanto outra requisição é feita. Este tipo de código pode gerar pressão no pool de conexões com o banco de dados, por exemplo: dado que enquanto uma transação está aberta aquele ```EntityManager``` precisa de uma conexão ativa. 

E ainda no código acima realmente precisamos de duas transações, uma para persistir inicialmente e outra para atualizar o objeto. O que você poderia fazer?

## Informação de suporte

* Tenta dar uma olhada na classe ```TransacionTemplate``` [na documentação do Spring](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/transaction/support/TransactionTemplate.html)
* [É importante você entender também que se você tiver utilizado um Repository, o comportamento default é rodar uma transação por método.](https://domineospring.wordpress.com/2019/10/17/transacoes-nao-devem-ser-habilitadas-por-default/) Este é um texto escrito por Alberto tentando mostrar os perigos de você deixar transações habilitadas por default.

