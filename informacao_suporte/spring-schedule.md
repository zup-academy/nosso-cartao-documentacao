# Como fazer operações em segundo plano utilizando o Spring?

Já sabemos a diferença entre síncrono e assíncrono, correto!?

Se não, não tem problema! [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/synchronous-vs-asynchronous.md)

Vamos começar nosso tutorial de como agendar tarefas no Spring?

1º Precisamos habilitar a funcionalidade no Spring, para isto adicione a anotação [@EnableScheduling](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/scheduling/annotation/EnableScheduling.html) 
na classe de inicialização do seu sistema, ou seja, na classe que tem o método `main`, como por exemplo no código abaixo:

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

No código de exemplo foi criado a função da nossa tarefa, porém não é o suficiente!

3º Precisamos dizer para o Spring que está classe é uma tarefa e que precisa executar o método `executaOperacao` a cada 1 segundo, para 
isto, precisamos adicionar duas anotações: [@Component](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Component.html) 
e [@Scheduled](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/scheduling/annotation/Scheduled.html)
, conforme código abaixo:

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

## Conhecendo a anotação

Sempre quando aprendemos algo é super importante ir mais fundo, e quando falamos de Anotações, por exemplo, existem 
várias configurações que podem atender seu cenário!

Vamos aprender mais sobre a anotação [@Scheduled](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/scheduling/annotation/Scheduled.html)?

No exemplo acima a gente utilizou o atributo `fixedDelay`, o que ele faz? qual objetivo?

O atributo `fixedDelay` execute o método anotado com um período fixo em milissegundos entre o final da última chamada e o 
início da próxima.

Existem outros atributos, como por exemplo:

- **fixedRate:** Execute o método anotado com um período fixo em milissegundos entre chamadas.
- **initialDelay:** Número de milissegundos a atrasar antes da primeira execução de uma tarefa.

Super bacana né! Temos várias possibilidades e aplicabilidade em apenas uma anotação!

## Melhores práticas

No exemplo acima a gente colocou para executar a cada um segundo a operação, mais o cliente mudou de ideia e necessita 
que seja a cada hora!

Muito fácil né! Só alterar no código, compilar, fazer testes, release e deploy e em 3 dias está pronto!

Três dias por conta de alterar uma linha de código, não parece bom!

Pensando nisso o Spring permite você definir a periodicidade via propriedade, que demais né! Vamos fazer isto!?

1º Precisamos definir nossa propriedade no arquivo `application.properties`, conforme exemplo abaixo:

```properties
periodicidade.executa-operacao=1000
```

2º Precisamos passar essa propriedade para a anotação @Scheduled, conforme código abaixo:

```java
@Scheduled(fixedDelayString = "${periodicidade.executa-operacao}")
```

Não entendeu, não tem problema! Vamos explicar melhor!

Para cada possibilidade de configuração na anotação @Scheduled existe a mesma via String, como por exemplo:

- initialDelayString
- fixedRateString
- fixedDelayString

Isso possibilita a gente usar a expressão do Spring para passar valores da propriedade, conforme abaixo:

```
${NOME_DA_PROPRIEDADE}
```

Exemplo

```java
@Scheduled(fixedDelayString = "${periodicidade.executa-operacao}")
```

Demais né!? Sim, porém caímos no mesmo problema, vai levar dias!

Vamos melhorar isso? Estamos a um passo de fazer uma revolução!

Vamos falar de variável de ambiente?

Uma variável de ambiente é um valor nomeado dinamicamente que pode afetar o modo como os processos em execução irão se 
comportar em um computador, ou seja, se tiver uma variável de ambiente que representa a periodicidade, basta alterar ela.
 
Assim a gente não precisa modificar o código e passar por todo ciclo de desenvolvimento, ganhando muito tempo!

Talvez você esteja pensando, como receber uma variável de ambiente utilizando Spring?

No spring para receber um valor de uma variável de ambiente, basta definir nossa propriedade, como por exemplo:

```properties
periodicidade.executa-operacao=${NOME_DA_VARIAVEL_DE_AMBIENTE}
```

Dessa forma fica obrigatório ter essa propriedade para executar nossa aplicação, isso é ruim!

Não seria legal termos um valor padrão, caso não existir a variável de ambiente?

Para isto, precisamos definir o valor padrão, conforme exemplo abaixo:

```properties
periodicidade.executa-operacao=${NOME_DA_VARIAVEL_DE_AMBIENTE:VALOR_PADRÃO}
```

Exemplo

```properties
periodicidade.minha-tarefa=${PERIODICIDADE_MINHA_TAREFA:1000}
```

Analisando a propriedade sabemos que se não existir a variável de ambiente `PERIODICIDADE_MINHA_TAREFA` o valor padrão 
será um segundo, demais né!

Aplicando isso, podemos economizar muito tempo, pois agora leva-se minutos ao invés de dias para fazer o ajuste solicitado 
pelo cliente.

**Importante**

Você sabia que foi aplicado um dos fatores do The Twelve Factor App?

Você aplicou o fator III. Configurações, na qual diz que você deve armazenar as configurações no ambiente!

Quer saber mais?  Acesse o [link!](https://12factor.net/pt_br/config)

# Informação de Suporte

Quer saber mais sobre Spring Schedule, acesse o [link!](https://docs.spring.io/spring/docs/current/spring-framework-reference/integration.html#scheduling-annotation-support)

Quer saber mais sobre The Twelve Factor App, acesse o [link!](https://12factor.net/pt_br/)