# Como utilizar Micrometer no Spring?

O Spring Boot Actuator fornece gerenciamento de dependência e configuração automática para o [Micrometer](https://micrometer.io/)
, uma biblioteca de métricas de aplicativos que suporta vários sistemas de monitoramento, incluindo:

- [Prometheus](https://prometheus.io/)
- [Datadog](https://docs.datadoghq.com/metrics/)
- [Dynatrace](https://www.dynatrace.com/)

Dentre outros, gostaria de saber a lista completa? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-metrics)

Já sabemos que o Spring em conjunto com o Micrometer, suporta vários sistemas de monitoramento de métrica!

Talvez você esteja pensando em quais são os tipos de métricas, pois bem, o Micrometer provê os seguintes tipos:

- Counter
- Timer
- Guage

Vamos praticar?

Antes precisamos aprender sobre o objeto `MeterRegistry` que é a classe principal para criar métricas, no Spring ele 
já está configurado, portanto precisamos somente receber no construtor, conforme código abaixo:

```java
@Component
class MinhasMetricas {
    
    private final MeterRegistry meterRegistry;

    public MinhasMetricas(MeterRegistry meterRegistry) {
    this.meterRegistry = meterRegistry;    
    }

}
```

Agora que sabemos sobre o `MeterRegistry` é hora de explorar os tipos de métricas, vamos começar pelo contador?

## Métrica tipo Counter

Contadores relatam uma única métrica, uma contagem. A interface do contador permite aumentar em um valor fixo, que 
deve ser positivo!

Imagina que precisamos de uma métrica de números de propostas criadas, isso irá ajudar muito o pessoal de negócio a 
identificar qual emissora ou banco utilizam mais o sistema!

Vamos fazer isto? Para essa tarefa precisamos utilizar o MeterRegistry e o método de criação de contador, conforme código 
abaixo:

```java
public void meuContador() {
    Collection<Tag> tags = new ArrayList<>();
    tags.add(Tag.of("emissora", "Mastercard"));
    tags.add(Tag.of("banco", "Itaú"));

    Counter contadorDePropostasCriadas = this.meterRegistry.counter("proposta_criada", tags);
    
}
```

Criamos nosso contador, demais né!

Agora vamos incrementar o mesmo, para isto existe um método denominado `increment`, conforme código abaixo:

```java
contadorDePropostasCriadas.increment();
```

Pronto agora temos um contador, precisamos achar uma maneira de estimular o mesmo! O que acha de colocar na sua API de 
criar proposta?

Para testar, precisamos criar algumas propostas!

Após criar as propostas, vamos abrir o endereço `http://localhost:8080/actuator/prometheus` em seu navegador e procurar 
pelo nome da métrica `proposta_criada`, como é um contador o Micrometer irá adicionar no final a palavra `total`, 
portanto, o nome da métrica será `proposta_criada_total`.

Achou a métrica? Ficou algo parecido conforme o exemplo abaixo?

```
# HELP proposta_criada_total  
# TYPE proposta_criada_total counter
proposta_criada_total{banco="Itaú",emissora="Mastercard",} 44.0
```

Eba! Aprendemos como criar uma métrica de contador! Vamos aprender outra?

## Métrica tipo Timer

Os temporizadores destinam-se a medir latências de curta duração e a frequência desses eventos. Todas as implementações 
do Timer relatam pelo menos o tempo total e a contagem de eventos como séries temporais separadas. 

Imagina que a API de consultar proposta está demorando demais, segundo os clientes, porém não temos métricas para saber 
se tem relação com o horário da consulta, quantidade de usuário, etc.

Vamos criar uma métrica? Para essa tarefa precisamos utilizar o MeterRegistry e o método de criação de temporizadores, 
conforme código abaixo:

```java
Collection<Tag> tags = new ArrayList<>();
tags.add(Tag.of("emissora", "Mastercard"));
tags.add(Tag.of("banco", "Itaú"));

Timer timerConsultarProposta = this.meterRegistry.timer("consultar_proposta", tags);
timerConsultarProposta.record(() -> {
    // Método da sua operação
    consultarProposta();
});
```

Pronto agora temos um temporizador, precisamos achar uma maneira de estimular o mesmo! O que acha de colocar na sua API de 
consultar proposta?

Para testar, precisamos consultar algumas propostas!

Após consultar as propostas, vamos abrir o endereço `http://localhost:8080/actuator/prometheus` em seu navegador e procurar 
pelo nome da métrica `consultar_proposta`, como é um temporizador o Micrometer irá criar duas métricas e adicionar no 
final a palavra `count` e  `sum`, portanto, o nome da métrica será `consultar_proposta_seconds_count` 
e `consultar_proposta_seconds_sum`.

Achou a métrica? Ficou algo parecido conforme o exemplo abaixo?

```
# HELP consultar_proposta_seconds  
# TYPE consultar_proposta_seconds summary
consultar_proposta_seconds_count{banco="Itaú",emissora="Mastercard",} 12.0
consultar_proposta_seconds_sum{banco="Itaú",emissora="Mastercard",} 36.003066791
```

Talvez esteja se perguntando o motivo de ter duas métricas?

Com as duas métricas conseguimos responder quantas consultas foram feitas (12) e quantos segundos elas demoraram em 
média (36 / 12 = 3s) no período selecionado, demais né!?

Eba! Aprendemos como criar uma métrica de temporizador! Vamos aprender outra?

## Métrica tipo Gauge

# Informação de Suporte

Está em dúvida de como configurar o Spring Boot Actuator? [Aqui você encontra como fazer isto!](../informacao_suporte/spring-actuator.md)

Está em dúvida de como configurar o Micrometer? [Aqui você encontra como fazer isto!](../informacao_suporte/spring-actuator-metrics.md)

Talvez esteja pensando sobre segurança no Spring Boot Actuator? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_suporte/spring-actuator-security.md)

Quer saber mais sobre Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-enabling)

Quer saber mais sobre o The Twelve-Factor App? Acesse o [link!](https://12factor.net/pt_br/)