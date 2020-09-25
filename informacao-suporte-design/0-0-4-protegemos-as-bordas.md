# Protegemos as bordas do sistemas como se não houvesse amanhã. Principalmente a mais externa

Todo dado que entra em algum método do nosso sitema é potencialmente inválido. Por que você vai executar o código sem garantir que os parâmetros de entrada estão validos? Quando falamos da borda mais externa então, o cuidado é redobrado. Não controlamos nada do lado do cliente e não assumimos que nada está válido.

```java
	@PostMapping(value = "/propostas")
	@Transactional
	public ResponseEntity<?> cria(
			@RequestBody @Valid NovaPropostaRequest request) {
                //codigo que vai rodar em função dos parâmetros recebidos
            }
    }

    public class NovaPropostaRequest {

        private String email;
        private String nome;
        private String endereco;
        private BigDecimal salario;
        private String documento;  

        //construtor
    }  
```

Se você olhar para cima, como vai saber que o email é valido? E como vai saber que o nome não está em branco? O código que está dentro do método do controller só deveria rodar se as informações contidas no objeto que representa a request estiverem válidos. Fique sempre com isso na cabeça. Do mesmo jeito que você não aceita encomenda com caixa aberta, você não aceita parâmetros com valores inválidos. 

Todos os frameworks maduros do mercado suportam algum mecanismo de validação integrado. O Spring não seria diferente. Ele tem um módulo chamado Spring Validation e que permite que você crie validações específicas e também se integre com a especifcação Bean Validation. 

