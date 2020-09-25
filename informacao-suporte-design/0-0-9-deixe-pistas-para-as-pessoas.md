# Deixe pistas onde não for possível resolver com compilação

**Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação.**

[Quando falamos do uso de construtor para forçar a passagem das informações naturais e obrigatórias](./construtor-para-informacao-natural.md), deixamos um exemplo de código. Vou lembrá-lo para você aqui:

```java
    @Deprecated
	public Autor() {

	}

	public Autor(String nome, String email,
			String descricao) {
		this.nome = nome;
		this.email = email;
		this.descricao = descricao;
	}
```

E aí, no outro ponto do sistema, tinha a chamada para o construtor com argumentos.

```java
	public Autor toModel() {        
		return new Autor(this.nome,this.email,this.descricao);
	}
```

Olhando só para ponto da chamada, como podemos saber se o nome ou descrição tem algum limite de tamanho, ou mesmo que o email tem o formato de email? Infelizmente não temos como fazer isso em tempo de compilação em nenhuma linguagem que seja amplamente utilizada no mercado, como Java ou C#. 

Dado que não temos a melhor opção que é travar em tempo de compilação, podemos usar mecanismos da linguagem para deixar dicas. 

```java
    public Autor(@NotBlank String nome, @NotBlank @Email String email,
			@NotBlank @Size(max = 400) String descricao) {
		this.nome = nome;
		this.email = email;
		this.descricao = descricao;
	}
```

Perceba que agora usamos algumas annotations da Bean Validation para deixar uma dica das restrições dos parâmetros necessários para a criação de um autor. Você poderia acrescentar comentários também. 

## Ouvi falar que deixar comentários ou pistas é ruim?

Talvez você já tenha ouvido falar algo assim: Se um código precisa de comentário então quer dizer que ele não está bem escrito. Então qual o motivo para projeto open source que sonha ser importante no planeta ter uma documentação muito boa? Inclusive os projetos open source da ZUP tem uma excelente documentação! 

Deixar uma pista em forma de comentário, annotation ou alguma outra forma não significa que você vai explicar a implementação da coisa. Apenas você quer ajudar a próxima pessoa que pegar aquele código para que ela tenha mais facilidade de entendimento. 

## Essas validações de annotations vão ser executadas automaticamente?

Agora que eu deixei umas annotations de validação nos parâmetros do construtor, será que quando eu rodar o código abaixo a validação vai acontecer automaticamente?

```java
	public Autor toModel() {        
		return new Autor(this.nome,this.email,this.descricao);
	}
```

Deveria, mas infelizmente não. As annotations da Bean Validation não fazem parte do runtime padrão do Java e não existe nenhum hook do compilador para gerar o bytecode necessário para executar a validação. É realmente uma pena. Então, por agora, elas realmente servem para deixar dicas no código. 


