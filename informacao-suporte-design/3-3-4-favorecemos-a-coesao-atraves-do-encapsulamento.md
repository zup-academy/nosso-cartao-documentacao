# Favorecemos a coesão através do encapsulamento.

Operações sobre dados cujo tipo é padrão da linguagem devem ficar dentro das nossas classes.

Lá na raiz da orientação a objetos, no paper Programming with Abstract Data Types, é explicado que a ideia de uma classe nasce da necessidade de representar um tipo que não é suportado pela linguagem de programação em si. Esse tipo é construído em cima dos tipos que já existem ou talvez em cima de outros tipos criados dentro do sistema, o que conhecemos como atributos.

Além disso também é explicado que agora esses tipos abstratos de dados devem ter funções que manipulam os seus próprios atributos, o que conhecemos como métodos. Toda operação sobre os atributos deve residir dentro da própria classe. Neste ponto está sendo sustentado talvez o principal motivo de criarmos um tipo abstrato de dados (classes): Ter um local onde restringimos o uso daquelas variáveis para aquelas operações. Estamos falando de juntar estado e comportamento. Essa junção tende a promover a coesão. 

Quando bem utilizado, o encapsulamento, além de promover a coesão, promove um jeito interessante de distribuir a dificuldade de entendimento entre várias das classes.

A pergunta que fica é: se unir é estado e comportamento é algo que pode ajudar no entendimento e também que está na base da criação da orientação a objetos, qual o motivo dos códigos não tirarem proveito ? A minha hipótese é que estamos esquecendo do jeito lógico de fazer a análise.

## Exemplo #1: Lógica de consulta de estado do objeto

```java
    final Bolao bolao = bolaoRepository.findById(this.idBolao).get();
    if (bolao.getDataExpiracao().isBefore(Instant.now())) {
        return ResultadoConfirmacao.conviteExpirado();
    }
```

Aqui temos uma lógica de verificação de data sobre um estado do objeto do tipo ```Bolao```.

O mesmo código poderia ter sido escrito da seguinte forma:

```java
final Bolao bolao = bolaoRepository.findById(this.idBolao).get();
    if (bolao.aceitaConvite()) {
        return ResultadoConfirmacao.conviteExpirado();
    }
```

Pode ser que seja necessário deixar o instante flexível. Para isso usamos os parâmetros.

```java
    final Bolao bolao = bolaoRepository.findById(this.idBolao).get();
    if (bolao.aceitaConvite(Instant.now())) {
        return ResultadoConfirmacao.conviteExpirado();
    }

    public class Bolao {
        //codigo omititdo
         
        public boolean aceita(Instant data) {
            return this.dataExpiracao.before(data);
        }         
    }
```


Quando você concentra toda lógica sobre um tipo padrão da linguagem que também representa o estado dentro da classe daquele objeto você aumenta as chances de distribuir a complexidade do código respeitando os limites de entendimento que você definiu derivado do CDD. 

### Por que você está falando sobre o tipo padrão da linguagem?

Porque essa é uma forma nítida de você ter um norte. No exemplo acima, DateTime é um tipo padrão do Java, então você concentra a lógica sobre ela dentro do seu tipo abstrato de dados(sua classe). 

Só que como ```DateTime``` também é um tipo abstrato de dados, aplicamos a mesma regra de concentrar a lógica sobre tipos fundamentais da linguagem dentro da classe que é dona deles. Perceba que não foi acessada a informação que guarda o instante no tipo ```DateTime``` para analisar se era anterior ao instante atual. Delegamos a chamada para um método pronto na própria classe ```DateTime```. Ou seja, a mesma regra foi aplicada.

Um outro exemplo onde podemos podemos fazer a mesma análise.

```java
    public Set<PaymentMethod> filterDesiredPaymentMethods(User user) {
        return this.paymentMethods.stream()
            .filter(paymentMethod -> user.getDesiredPaymentMethods().contains(paymentMethod))
            .collect(Collectors.toSet());
    }
```
Perceba que na linha ```user.getDesiredPaymentMethods().contains(paymentMethod))``` é acessado diretamente o tipo que referencia uma coleção e aí em seguida acessamos um método pronto. O problema é que esse tipo vive no ```User```. 

Aqui basta que seja aplicada a mesma regra: Operações sobre dados cujo tipo é padrão da linguagem devem ficar dentro das classes dos objetos. Neste caso, a coleção retornada pelo método ```getDesiredPaymentMethods``` é padrão da linguagem. Uma versão diferente do código pode ser a seguinte:

```java
    public Set<PaymentMethod> filterDesiredPaymentMethods(User user) {
        return this.paymentMethods.stream()
            .filter(user :: acceptsPayment)
            .collect(Collectors.toSet());
    }
```
Agora você tem um método no ```User``` que opera sobre o estado dele. Lá dentro, para operar sobre estado da coleção, é invocado o método contains. E dessa forma você vai distribuindo as operações do sistema, deixando a inteligência da aplicação dividida de uma forma que respeite nosso limite natural de entendimento. 

Por sinal, parece interessante ter um jeito lógico para aproximar os dados das operações, mas ainda não diminuimos de fato a dificuldade de entendimento em nenhum exemplo. Dada a métrica do CDD que considera branches e funções como argumento como pontos de complexidade, os exemplos acima ainda mantém suas pontuações, por mais que o código tenha ficado mais coeso.

## Exemplo #2: Coesão através do encapsulamento para atualização de objeto

Considere o seguinte trecho de código:

```java        
		if (student.getCoach() == null
				|| student.getCoach().getId().equals(assignedAdvisor)) {
			student.setCoach(personService.get(assignedAdvisor));
		}
```

Percebemos que o retorno do método ```getCoach``` é um tipo abstrato de dados. O código depois navega invoca o método ```getId()``` que retorna um tipo padrão da linguagem, no caso um ```Long```. Usando a nossa lógica para deixar o código mais coeso, movemos a operação sobre o **id** para dentro do tipo da variável ```student``` e poderíamos chegar no seguinte:

```java        
		if (student.hasSameId(assignedAdvisor)) {
			student.setCoach(personService.get(assignedAdvisor));
		}
```

O código ficou mais coeso, porém o ```ìf``` continua no mesmo ponto de código e a dificuldade de entendimento ficou a mesma.

### Mal cheiro nas múltiplas chamadas de método em cima do mesmo objeto

No código logo acima, utilizamos a variável ```student``` para invocar o método ```hasSameId``` e também é utilizada a mesma variável para invocar o método ```setCoach```. O mesmo código poderia ser escrito da seguinte forma:

```java
    student.tryToChangeCoach(assignedAdvisor,personService);
```

Agora o código removeu um ```if``` de determinado ponto e moveu para outro lugar, literalmente distribuindo a dificuldade de entendimento pelo sistema. E ainda de quebra conseguimos fazer sem criar uma classe nova, apenas usamos um tipo que já existia. Claro que precisamos ficar de olho nos limites de entendimento que foram estabelecidos. 

## Uma entidade pode acessar um service?

Em primeiro lugar eu preciso que você preste bastante atenção na próxima frase: Você pode fazer o que quiser no código se souber analisar o lado positivo e negativo de cada decisão. Você precisa sempre ficar atento as duas coisas principais, respeitando a ordem de prioridde

1. A prioridade é funcionar
2. Vai ser bom se funcionar e se outras pessoas puderem entender

Dito isso, o método ```tryToChanceCoach``` ficaria da seguinte forma:

```java   
    public class Person {
        //atributos aqui

        public Person tryToChangeCoach(UUID assignedAdvisor,PersonService personService) {
            if (this.coach == null
                    || this.coach.hasSameId(assignedAdvisor)) {
                this.coach = personService.get(assignedAdvisor);                
            }

            return this.coach;
        }
    }
```

Esqueça qualquer coisa que uma classe terminada com o sufico *Service* possa dizer para você. Em geral você tem dois tipos de classes no código:

* As que tem atributos de dados
* As que tem atributos de depedência

Enquanto a ```Person``` é uma classe que tem atributos de dados, a ```PersonService``` é uma classe que tem atributos de dependência. Elas estão conversando. Um ponto de atenção é que a ```PersonService``` tem muitos métodos e é uma classe utilizada em muitos pontos do código. 

Já conversamos sobre API's não democráticas então aqui é um momento que você pode combinar técnicas. Para que o método ```tryToChangeCoach``` não fique conectado com uma interface possivelmente instável, podemos criar uma nova, específica e muito mais estável.

```java   
    public interface GetPersonByUUID {
        Person get(UUID id);
    }

    public interface PersonService extends GetPersonByUUID {
        //não precisa mexer em nada aqui
    }

    public class Person {
        //atributos aqui

        public Person tryToChangeCoach(UUID assignedAdvisor,GetPersonByUUID getPersonByUUID) {
            if (this.coach == null
                    || this.coach.hasSameId(assignedAdvisor)) {
                this.coach = getPersonByUUID.get(assignedAdvisor);                
            }

            return this.coach;
        }
    }
```

E a mágica está feita. Seu método ```tryToChangeCoach``` está conectado com um tipo bem específico e talvez a sua cabeça não fique jogando contra você :). 