# Só alteramos estado de referências que criamos.

A prática completa é: **Só alteramos estado de referências que criamos. Não mexemos nos objetos alheios. A não ser que esse objeto seja criado para isso, como é o caso de argumentos de métodos de borda mais externa. Estes são, geralmente, associados a frameworks.**

Esta prática tem muita influência do mundo funcional e tem a ver com imutabilidade. Enquanto que em linguagens funcionais todas as estruturas já nascem com a ideia de imutabilidade, nas outras linguagens a mutabilidade é cidadã de primeiro nível. Abaixo temos um exemplo do que queremos evitar:

```java
    public EarlyAlert create(@NotNull final EarlyAlert earlyAlert){
        //mais codigo aqui para cima

        final Person person = earlyAlert.getPerson();

		if (person.getCoach() == null
				|| assignedAdvisor.equals(person.getCoach().getId())) {
			person.setCoach(personService.get(assignedAdvisor));
		}  

        //mais codigo aqui para baixo      
    }
```

Este código foi extraído de um projeto open source, público no github. 

O método recebe como argumento uma referência para um objeto do tipo ```EarlyAlert```. Dentro do método, ele recupera uma outra referência para o tipo ```Person``` que, neste contexto, representa um estudante. Neste momento foque só no que o código faz e não se ele poderia ser escrito de outra forma :). 

Perceba que caso a condição testada no ```if``` retorne ```true```, a referência para o objeto do tipo ```Person```, que foi extraída da objeto do tipo ```EarlyAlert```, vai ser alterada. 

E qual o problema que podemos ter aqui? Este trecho de código, é invocado a partir deste outro ponto aqui. 

```java
    private boolean createEarlyAlert(Person person, SuccessIndicator    successIndicator) {
        //um novo EarlyAlert é criado
        EarlyAlert earlyAlert = new EarlyAlert();
        earlyAlert.setPerson(person);        
        earlyAlert.setCampus(getCampus(person));
        earlyAlert.setCourseTermCode(getCurrentOrNextTerm());

        //chamou o método que pode alterar a Person que foi definida no
        //EarlyAlert
        earlyAlertService.create(earlyAlert);

        //você não tem garantia que a person retornada é a mesma de antes
        //da chamada do método e nem se as informações da Person são as //////mesmas.
        Person person2 = earlyAlert.getPerson()
    }
```

## Alterar referências alheias complica todo acompanhamento do estado

Uma vez que o código do seu sistema aceita que referências de origem desconhecida sejam alteradas, você perde completamente a habilidade de "*trackear*" estado pela aplicação. Um objeto pode ter seu estado alterado em qualquer lugar e, a partir daí, seu **encapsulamento cai como um castelo de cartas**. O tempo inteiro você vai precisar entrar nos métodos que está chamando para verificar se alguém mexendo no objeto que você criou. 

Você deve evitar com todas as suas forças alterar referências criadas em outros lugares. **Só quem mexe numa referência é o ponto do código que a criou.**

## Como solução alternativa, deixe dicas de que algo foi alterado

O método ```create```, que altera o estado do objeto do tipo ```EarlyAlertService``` poderia deixar uma dica para quem chama, informando que aquele objeto não é mais o mesmo. 

```java
    public Modified<EarlyAlert> create(@NotNull final EarlyAlert earlyAlert){
        //mais codigo aqui para cima

        final Person person = earlyAlert.getPerson();

		if (person.getCoach() == null
				|| assignedAdvisor.equals(person.getCoach().getId())) {
			person.setCoach(personService.get(assignedAdvisor));
		}  

        //mais codigo aqui para baixo   
        return new Modified(earlyAlert);   
    }
```

Agora o retorno do método deixa claro que ele mexe no que não é da conta dele. Dessa forma, o ponto do código que realiza a invocação já tem uma ideia do que está acontecendo. E quando você olha para o fluxo como um todo, também consegue ter uma ideia dos pontos que alteram estado de referências desconhecidas. 

## Também deixe dicas sobre alterações em sistemas externos

Agora que abraçamos a ideia de não alterar referências alheias inspirado pelo princípio da imutabilidade, podemos tentar levar a mesma ideia para alterações de sistemas externos, como banco de dados e outras aplicações que possamos usar. 

O gargalo da imutabilidade pura para a maioria dos sistemas, é que em algum ponto ele é mutável. Por exemplo, o seu banco de dados. Todos os bancos de dados famosos do planeta são mutáveis e isso deveria ser levado em conta dentro da nossa prática. Pegue esse código como exemplo:

```java
	public Pagamento executa(Long idPedido,
			@Valid NovoPagamentoOnlineRequest request) throws BindException {		

        Pagamento novoPagamento = request.toPagamento(idPedido, valor,
        manager);
		Pagamento novoPagamentoSalvo = executaTransacao.commi(novoPagamento);

        return novoPagamentoSalvo;
		}
				
	}
```

Este método é chamado daqui:

```java
	@PostMapping(value = "/pagamento/online/{idPedido}")
	public void paga(@PathVariable("idPedido") Long idPedido,
			@RequestBody @Valid NovoPagamentoOnlineRequest request)
			throws Exception {
		Pagamento novoPagamento = iniciaPagamento.executa(idPedido,
				request);
	}
```

Como podemos saber que o ```Pagamento``` retornado foi salvo no banco de dados? Ou salvo em qualquer outro lugar? Não tem como saber. Ou você entra no método para entender, ou corre o risco de até salvar duas vezes. 

Aqui temos um ponto do código, diferente do ponto da entrada de dados, alterando sistemas externos. O contexto muda, mas a regra permanece: **só a entrada do dado deveria alterar sistemas externos**. Caso não seja possível abraçar a ideia, como o exemplo acima, você pode usar a ideia das dicas de código de novo. 

```java
	public Persisted<Pagamento> executa(Long idPedido,
			@Valid NovoPagamentoOnlineRequest request) throws BindException {		

        Pagamento novoPagamento = request.toPagamento(idPedido, valor,
        manager);
		Pagamento novoPagamentoSalvo = executaTransacao.commi(novoPagamento);

        return new Persisted(novoPagamentoSalvo);
		}
				
	}
```

Agora o ponto do sistema que invoca este método sabe que vai receber um objeto persistido. Com clareza sobre essa informação, você diminui as chances de refazer algo que já aconteceu. 

## Explicite a dificuldade

Nem sempre fácil manter tudo organizado e está tudo bem. O seu código precisa ser honesto em relação as dificulddes e deixar isso claro para a próxima pessoa. Lembre que ainda estamos na era que seres humanos mantém o código e, enquanto isso durar, precisamos construir sistemas que executem em máquinas e sejam possíveis de entender por pessoas. 




