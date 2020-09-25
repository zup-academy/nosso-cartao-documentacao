# Não usamos exception para controle de fluxo.

Exceptions foram criadas para que casos não imaginados possam ser tratados e um sinal enviado para o programa que ele deve interromper o fluxo de execução. 

```java

	protected BeanWrapper createBeanWrapper() {
		if (this.target == null) {
			throw new IllegalStateException("Cannot access properties on null bean instance '" + getObjectName() + "'");
		}
		return PropertyAccessorFactory.forBeanPropertyAccess(this.target);
	}

```

Acima temos um código retirado de uma versão do framework Spring, um método da classe ```BeanPropertyBindingResult```. A classe tem um atributo que, no momento da invocação do método ```createBeanWrapper``` nunca deveria estar nulo. Mas é claro que existe uma diferença entre o que a gente quer e o que acontece de fato, então o código faz uso de técnicas de programação defensiva e verifica se o atributo ```target``` ainda está nulo. No caso da variável estar nula, temos uma situação estranha e não queremos que o código continue, por isso lançamos uma *exception*. 

Perceba, literalmente queremos que aquele fluxo seja terminado, encontramos um **bug** e não vamos deixar nosso sistema operar sobre uma situação que pode gerar problemas inesperados.

Uma *exception* é como um *goto*, um hack da linguagem poderoso para você conseguir quebrar o fluxo de execução de qualquer ponto. 

## Efeito colateral #1: Talvez custe performance

Na linguagem Java, por exemplo, sempre que você cria uma instância de ```Exception``` olha o que acontece lá por baixo dos panos:

```java
    public class Throwable {
     public Throwable() {
        fillInStackTrace();
     }

     private native Throwable fillInStackTrace(int dummy);
    }
   

    public class Exception extends Throwable{
        public Exception(){
            //chama o construtor de Throwable
            super();
        }
    }
```

Toda a pila de execução é colocada dentro da nova instância, o que pode ser custoso para sua aplicação caso a exception seja lançada múltiplas vezes por intervalo de tempo. Quando mais profundo é o ponto de lançamento da exception, maior vai ser a pilha de execução criada. 

Claro que as máquinas virtuais e ambientes de execução em geral vão evoluindo muito com o tempo, mas com certeza é um ponto de atenção. 

## Efeito colateral #2: Ponto de tratamento do problema

Como a *exception* é um hack da linguagem, literalmente um *goto*, você pode tratar aquilo onde bem entender. Por exemplo, vários frameworks fornecem mecanimos para você tratar exceptions de maneira genérica. 

```java    
    @ExceptionHandler(BindException.class)
    public ValidationErrorsOutputDto handleValidationError(BindException exception) {
    	
        // codigo omitido
    }
```

No Spring MVC você pode criar um método, adicionar a configuração dizendo que você quer capturar toda *exception* que seja igual ou filha de ```BindException``` e fazer o que quiser a partir dali. Ou seja, em qualquer ponto do seu código que tenha sido invocado em função da execução de um método de controller, você pode lançar essa exception e ela vai cair aqui. 

E aí temos um caso clássico do mercado:

```java    
    @ExceptionHandler(BusinessException.class)
    public ValidationErrorsOutputDto handleBusinessException(BusinessException exception) {
    	
        // codigo omitido
    }
```
Situações esperadas dentro do fluxo de negócio, que poderiam ser tratadas com retornos convencionais, lançam exceptions para pular de um ponto de código para outro. 

## Efeito colateral #3: Aumento de complexidade de entendimento

Cada classe de *exception* criada aumenta um ponto de complexidade no sistema como um todo e o seu uso aumenta um ponto de complexidade naquela unidade de código em específico. 

Além disso, se tem exception, pode ter ```try```, ```catch``` e talvez um ```finally```, o que traz mais três branches de código para sua análise. O que também, dada a nossa métrica derivada do CDD, aumenta a complexidade de entendimento. 

## Efeito colateral #4: No mundo das exceptions de runtime, perdemos clareza

Hoje em dia, mesmo no Java, o uso de *exceptions* ficou restrito ao tipo de que não força um tratamento explícito no código. Dessa forma criamos várias situações onde os possíveis retornos não ficam claros. Abaixo, temos um exemplo clássico:

```java
	public void abateEstoque(@Positive int quantidade) {
		//uma situação inesperada
		Assert.isTrue(quantidade > 0,
				"Olha, não podemos abater quantidade menor ou igual a zero "
						+ quantidade);
		
		//situacao esperada. Pq se não fosse esperada, não teria o if
		if(this.estoque < quantidade) {
			throw new EstoqueException("Acabou o estoque");
		}
		this.estoque -= quantidade;		
	}
```

O ponto do código que invoca o método acima não tem como saber que tal invocação pode lançar uma *exception*. Claro que podíamos ter deixado uma dica:

```java
    /**
    ** @throws EstoqueException quando não tiver estoque suficiente
    **/
	public void abateEstoque(@Positive int quantidade) {
		//uma situação inesperada
		Assert.isTrue(quantidade > 0,
				"Olha, não podemos abater quantidade menor ou igual a zero "
						+ quantidade);
		
		//situacao esperada. Pq se não fosse esperada, não teria o if
		if(this.estoque < quantidade) {
			throw new EstoqueException("Acabou o estoque");
		}
		this.estoque -= quantidade;		
	}
```

A dica ajudaria, mas sempre que for possível tratar a situação com uma trava de compilação. 

Especificamente na situação acima, seria até simples. Basta que o método retorne *boolean*. 

```java

    /**
    ** @return true se conseguir abater o estoque.
    **/
	public boolean abateEstoque(@Positive int quantidade) {
		//uma situação inesperada
		Assert.isTrue(quantidade > 0,
				"Olha, não podemos abater quantidade menor ou igual a zero "
						+ quantidade);
		
		//situacao esperada. Pq se não fosse esperada, não teria o if
		if(this.estoque < quantidade) {
			return false;
		}
		this.estoque -= quantidade;		
        return true;
	}
```

Não que já esteja 100% claro, dado que um *boolean* é um tipo padrão da linguagem Java e a semântic que ele carrega é de true ou false e isso, não necessariamente indica que o estoque foi abatido ou não. Só que aí juntamos com uma dica e fica um pouco melhor. 

## Possibilidade de utilizar retornos explícitos

Agora algumas situações hipóteticas para pensarmos:

* E se a gente também precisasse retornar um objeto representando a ideia de estoque abatido para indicar a hora exata da operação?
* E se a também gente precisasse ter um retorno indicando que o estoque zerou?
* E se a gente precisasse combinar os dois requisitos de cima?

Para estas necessidades o retorno booleano deixaria de ser suficiente. Agora temos uma situação onde precisamos retornar algo em caso positivo e outra coisa no caso negativo. Talvez cair para a *exception* esteja passando na sua mente. Tudo bem se tiver. Dessa vez vamos por um caminho diferente, vamos nos inspirar numa abstração da linguagem Scala chamada ```Either``` que, na verdade, é inspirada na abstração de mesmo nome da linguagem [Haskell](https://hackage.haskell.org/package/base-4.14.0.0/docs/Data-Either.html). 

A ideia é que você a gente possa construir um objeto que tenha dois possíveis retornos, uma para sucesso e outro para erro. Em função disso, podemos chegar nesse código aqui:

```java
	public ResultadoAbateEstoque abateEstoque(@Positive int quantidade) {
		//uma situação inesperada
		Assert.isTrue(quantidade > 0,
				"Olha, não podemos abater quantidade menor ou igual a zero "
						+ quantidade);
		
		//situacao esperada. Pq se não fosse esperada, não teria o if
		if(this.estoque < quantidade) {
			return ResultadoAbateEstoque.vazio();
		}
		this.estoque -= quantidade;
		
		if(this.estoque == 0) {
			return ResultadoAbateEstoque.estoqueNoLimite(this,quantidade);
		}
		return ResultadoAbateEstoque.estoqueAbatido(this,quantidade);
	}
```

A classe ```ResultadoEstoqueAbatido``` fica assim:

```java
public class ResultadoAbateEstoque {
	
	private boolean vazio;
	private Produto produto;
	private @Positive int quantidade;
	private boolean estoqueNoLimite;

	private ResultadoAbateEstoque() {
		this.vazio = true;
	}

	private ResultadoAbateEstoque(Produto produto, @Positive int quantidade,boolean estoqueNoLimite) {
		this.produto = produto;
		this.quantidade = quantidade;
		this.estoqueNoLimite = estoqueNoLimite;
		
	}

	public static ResultadoAbateEstoque vazio() {
		return new ResultadoAbateEstoque();
	}

	public static ResultadoAbateEstoque estoqueNoLimite(Produto produto,
			@Positive int quantidade) {
		return new ResultadoAbateEstoque(produto,quantidade,true);
	}

	public static ResultadoAbateEstoque estoqueAbatido(Produto produto,
			@Positive int quantidade) {
		return new ResultadoAbateEstoque(produto,quantidade,false);
	}

	public boolean taVazio() {
		return vazio;
	}

	public boolean taNoLimite() {
		return this.estoqueNoLimite;
	}

	public EstoqueAbatido get() {
		Assert.isTrue(vazio,"Você não deveria buscar o estoque porque na verdade nao parece ter estoque");
		return new EstoqueAbatido(produto, quantidade);
	}

}
```

Agora, no ponto de invocação do método que abate o estoque você tem um retorno explícito e pode operar nele como quiser. A complexidade do código como um todo, pode até ficar parecida com o uso das exceptions, já que vamos ter controle de fluxo com o uso de ```if```. 

Só que agora ganhamos retorno explícito e temos usamos a compilação para indicar os possíveis caminhos do código. Entra aqui também a ideia de API's não democráticas. 

## Resumo da ópera

A parte boa do código é que podemos resolver o mesmo problema de N maneiras. A parte ruim do código é que podemos resolver o mesmo problema de N maneiras. 

Neste exato momento você tem mais uma ferramenta para usar na busca por soluções. Sabendo sempre o lado positivo e negativo de cada solução, fica muito mais fácil de tomar uma decisão. 
