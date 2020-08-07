# Padronização de erros seguindo as boas práticas de Orientação a Objetos?

Estamos construíndo um produto de geração de cartão, transação, etc. E algum parceiro tanto interno quanto externo gostaria 
de se integrar com a gente, ou seja, gostaria de usar nossas APIs e para que a integração seja o mais eficiente possível 
precisamos enriquecer nossas APIs com detalhes, inclusive no cenário de erro!

Portanto, precisamos fornecer o máximo possível de informação para que o parceiro identifique o que ele 
está fazendo de errado e consiga corrigir!

Ponto importante, quando falamos de enriquecer nossas APIs com o máximo de informação possível, lembre-se sempre da 
segurança, como por exemplo o erro `Número de cartão não existe`.

Quando um Hacker vê esse tipo de mensagem, ele pensa, vou ficar tentando um monte de número. Quando parar de dar esse 
erro, sei que é um número de cartão válido, o resto é história.

Estamos bem contextualizados, certo!?

Ainda não, quando falamos de APIs precisamos definir um modelo único de erro, para que seja uniforme em todas as APIs, 
assim o parceiro tem uma sensação de familiaridade e fica muito mais fácil outro sistema se integrar com o nosso produto!

Imagina só! Termos 10 APIs cada uma com um formato de erro diferente!

# Vamos fazer isso com Spring, então!

O Spring fornece uma forma de tratar todos os erros não tratados que aconteceram na camada da nossa API, ou seja, no 
nosso Controller, porém seguindo as boas práticas de orientação a objetos, não devemos lançar uma exceção com o objetivo 
de mapear um erro na API e ainda mais, ficando totalmente implícito para quem está dando manutenção, pois simplesmente 
você lança a exceção e ninguém trata e "magicamente" a sua API retorna um erro tratado.

Vamos fazer de uma forma explícita e que todos conseguem entender, sem ter que entender a fundo sobre Spring?

**1º** Precisamos definir como será o erro padrão em nossas APIs, aqui é apenas uma sugestão, no cenário real, devemos 
alinhar com a equipe!

```java
public class ErroPadronizado {

    private Collection<String> mensagens;

    // Getters, setters, construtor omitidos
}
```

Essa classe convertida em [JSON](https://www.json.org/json-en.html), ficaria assim:

```json
{
  "mensagens": [
    "Campo documento must not be blank",
    "Campo salario must not be null"
  ]
}
```

Muito intuitivo né!?

2º Precisamos definir o modelo de tratativa de erro, aqui é apenas uma sugestão, no cenário real, devemos alinhar 
com a equipe!

Um modelo legal e bastante intuitivo é um objeto de resultado da nossa operação, na qual retorna o status da operação, 
erro da operação, em cenário de erro, e o objeto criado, em caso de sucesso, conforme o código abaixo:

```java
public class ResultadoCriarProposta {

    private Proposta proposta;

    private Throwable excecao;


    public boolean temErro(){
        return excecao != null;
    }
    public Throwable getExcecao(){
        Asser.isTrue(temErro(),"Não deveria chamar caso não tenha erro");
        return excecao;
    }

    public Proposta getProposta(){
        Asser.isTrue(!temErro(),"Não deveria chamar caso tenha erro");
        return proposta;
    }    
}
```

Muito intuitivo né!?

3º Precisamos definir uma inteligência na camada do Controller ao receber o resultado do Serviço, conforme código abaixo:

```java
@PostMapping("/v1/api-test")
public ResponseEntity<?> post(@Validated @RequestBody CriarPropostaRequest criarPropostaRequest) {
    ResultadoCriarProposta resultadoCriarProposta = propostaService.criar(criarPropostaRequest);
    if (!resultadoCriarProposta.temErro()) {
        return ResponseEntity.status(HttpStatus.CREATED).body(resultadoCriarProposta.getProposta());
    } else {
        Collection<String> mensagens = new ArrayList<>();
        mensagens.add(resultadoCriarProposta.getExcecao().getMessage());

        ErroPadronizado erroPadronizado = new ErroPadronizado(mensagens);
        return ResponseEntity.status(HttpStatus.UNPROCESSABLE_ENTITY).body(erroPadronizado);
    }
}
```

Muito intuitivo né!?

Lembrando este código é apenas uma sugestão, lembre-se sempre de alinhar com sua equipe!

# Deixando a classe Resultado genérica

```java
/*
* E define o tipo de exception que vai ser trabalhada enquanto que S o tipo do objeto de sucesso.
*/
public class Resultado<E extends Exception,S> {

    private S sucesso;

    private E excecao;


    public boolean temErro(){
        return excecao != null;
    }
    public E getExcecao(){
        Asser.isTrue(temErro(),"Não deveria chamar caso não tenha erro");
        return excecao;
    }

    public S getProposta(){
        Asser.isTrue(!temErro(),"Não deveria chamar caso tenha erro");
        return sucesso;
    }

	public static <T> Resultado<Exception, T> sucesso(T objeto) {
		Resultado<Exception, T> resultado = new Resultado<Exception,T>();
		resultado.sucesso = objeto;
		return resultado;
	}

	public static <E extends Exception,T> Resultado<E, T> erro(E exception) {
		Resultado<E, T> resultado = new Resultado<E,T>();
		resultado.erro = exception;
		return resultado;
	}
}
```

Agora, com muita ajuda do uso dos generics do Java conseguimos criar uma classe que representa o resultado e que pode ser usada em qualquer lugar :). Um exemplo de uso:

```java
    Resultdo.sucesso(objeto);

    Resultado.erro(new Exception(...));
```


# Informação de Suporte

Gostaria de saber a padronização de erros utilizada pelo Spring Boot? [Aqui você encontra como fazer isso !!!](error-spring.md)

Gostaria de saber a padronização de erros utilizada pela Zup? [Aqui você encontra como fazer isso !!!](../informacao_suporte/error-zup.md)

Quer sabemos mais sobre Handler Advice, acesse o [link!](https://spring.io/blog/2013/11/01/exception-handling-in-spring-mvc)