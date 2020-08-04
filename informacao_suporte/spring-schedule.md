# Como fazer operações em segundo plano utilizando o Spring?

Já sabemos a diferença entre síncrono e assíncrono, correto!?

Se não, não tem problema! [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/synchronous-vs-asynchronous.md)

Vamos começar nosso tutorial de como agendar tarefas no Spring?

1º Precisamos habilitar a funcionalidade no Spring, para isto adicione a anotação [@EnableScheduling](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/scheduling/annotation/EnableScheduling.html) 
na classe de inicialização do seu sistema, ou seja, na classe que tem o método `main`, como por exemplo no código abaxio:

```java
@SpringBootApplication
@EnableScheduling
public class Application {

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }

}
```

2º Precisamos criar nossa tarefa, conforme código abaixo:

```java
public class MinhaTarefa {

    private void executaOperacao() {
        // Código omitido
    }

}
```

No código de exemplo foi criado a função da nossa operação, porém não é o suficiente!

3º Precisamos dizer para o Spring que está classe é uma tarefa e que precisa executar o método a cada X  tempos, para 
isto, precisamos adicionar duas anotações: [@Component](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Component.html) 
e [@Scheduled](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/scheduling/annotation/Scheduled.html) 
, conforme códgio abaixo:

```java
@Component
public class MinhaTarefa {

    @Scheduled(fixedDelay = 1000) \\ Tempo sempre em milisegundos!
    private void executaOperacao() {
        // Código omitido
    }

}
```

Para testar, vamos fazer algo simples! Vamos adicionar um log no método `executaOperacao`!

```java
System.out.println("Executando minha operação");
```

Iniciou sua aplicação!? Muito legal esse recurso, né!?

## Indo além

Sempre quando aprendemos algo é super importante ir mais fundo, e quando falamos de Anotações, por exemplo, existem 
várias configurações que podem atender seu cenário!

Vamos aprender mais sobre a anotação [@Scheduled](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/scheduling/annotation/Scheduled.html)?

No exemplo acima a gente utilizou o atributo `fixedDelay`, o que ele faz? qual objetivo?

O atributo `fixedDelay` execute o método anotado com um período fixo em milissegundos entre o final da última chamada e o 
início da próxima.

Existem outras anotações, como por exemplo:

- fixedRate: Execute o método anotado com um período fixo em milissegundos entre chamadas.
- initialDelay: Número de milissegundos a atrasar antes da primeira execução de uma tarefa.

Super bacana né! Temos várias possibilidades e aplicabilidade em apenas uma anotação!