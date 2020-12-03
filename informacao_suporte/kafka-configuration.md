# Spring Cloud Stream

Agora que sabemos o que é Apache Kafka e os seus conceitos, vamos aprender como configurar o mesmo utilizando Spring?

Vamos começar?

1º Precisamos adicionar a seguinte dependência em seu arquivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-stream-kafka</artifactId>
    <version>3.0.7.RELEASE</version>
</dependency>
```

2º Precisamos configurar as propriedades do Apache Kafka no arquivo `application.properties`:

```properties
# Endereço do Kafka
spring.kafka.bootstrap-servers=${KAFKA_HOST:localhost:9092}
```

Eba! Está tudo pronto! Vamos configurar nosso consumidor?

3º Precisamos configurar as propriedades do nosso consumidor, para isso, precisamos adicionar as seguintes propriedades 
no `application.properties`:

```properties
# Formato da chave (String) recebida!
spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer

# Formato da mensagem \ evento (JSON) recebida(o)!
spring.kafka.consumer.value-deserializer=org.springframework.kafka.support.serializer.JsonDeserializer

# Identificador do grupo de consumo
spring.kafka.consumer.group-id=${KAFKA_CONSUMER_GROUP_ID:minha-aplicacao}

# Modelo de coleta do consumidor (latest, earliest, none)
spring.kafka.consumer.auto-offset-reset=${KAFKA_AUTO-OFFSET-RESET:latest}
```

4º Precisamos definir nossa mensagem, como por exemplo, no código abaixo:

```java
public class EventoDeTransacao {

    private String id;

    private BigDecimal valor;

}
```

5º Precisamos configurar nosso consumidor, para isso, precisaremos criar nossa classe de configuração do Kafka, conforme 
código abaixo:

```java
@Configuration
public class KafkaConfiguration {

    private final KafkaProperties kafkaProperties;
    
    public KafkaConfiguration(KafkaProperties kafkaProperties) {
        this.kafkaProperties = kafkaProperties;
    }
    
}
```

Nossa configuração ainda não está pronta, precisamos configurar algumas coisas!

Nesse ponto, talvez esteja pensando? Nossa quanta configuração, eu só quero fazer um consumidor! 

Não se preocupe, no final, tudo vai fazer sentido!

Vamos continuar?

6º Precisamos adicionar as propriedades do nosso consumidor, na classe `KafkaConfiguration`, conforme código abaixo:

```java
public Map<String, Object> consumerConfigurations() {
    Map<String, Object> properties = new HashMap<>();
    properties.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, kafkaProperties.getBootstrapServers());
    properties.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
    properties.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, JsonDeserializer.class);
    properties.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getConsumer().getGroupId());
    properties.put(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, kafkaProperties.getConsumer().getAutoOffsetReset());

    return properties;
}
```

No código acima, a gente transcreveu as propriedades em um mapa de propriedades que será utilizado nos próximos passos!

7º Precisamos configurar nosso consumidor, na classe `KafkaConfiguration`, conforme código abaixo:

```java
@Bean
public ConsumerFactory<String, EventoDeTransacao> transactionConsumerFactory() {
    StringDeserializer stringDeserializer = new StringDeserializer();
    JsonDeserializer<EventoDeTransacao> jsonDeserializer = new JsonDeserializer<>(EventoDeTransacao.class, false);

    return new DefaultKafkaConsumerFactory<>(consumerConfigurations(), stringDeserializer, jsonDeserializer);
}
```

No código acima, a gente criou um `ConsumerFactory` que deve ser configurado em duas etapas, a primeira etapa a gente 
tem que definir qual será o desserializador da chave e do evento \ mensagem, como por exemplo, `StringDeserializer`, 
`JsonDeserializer`, etc. A segunda etapa e quais são as configurações desse consumidor, por este motivo foi criado o 
método `consumerConfigurations()`.

Demais né!?

Agora a nossa configuração do consumidor está tudo ok, vamos configurar nosso `listener`? 

8º Precisamos configurar nosso listener, na classe `KafkaConfiguration`, conforme código abaixo:

```java
@Bean
public ConcurrentKafkaListenerContainerFactory<String, TransactionMessage> kafkaListenerContainerFactory() {
    ConcurrentKafkaListenerContainerFactory<String, TransactionMessage> factory = new ConcurrentKafkaListenerContainerFactory<>();
    factory.setConsumerFactory(transactionConsumerFactory());

    return factory;
}
```

No código acima, a gente criou um `ConcurrentKafkaListenerContainerFactory`, no qual precisa ser cadastrado como ele irá 
tratar os eventos recebidos, por isso, foi criado o método `transactionConsumerFactory()`!

Demais né!? 

Vamos recapitular?

Primeiro a gente teve que transcrever as propriedades do consumidor para um mapa, que foi utilizado para definir nosso 
consumidor e por último foi cadastrado o nosso consumidor no listener!

Agora podemos fazer nosso listener que o mesmo saberá como lidar com o `EventoDeTransacao`, conforme código abaixo:

```java
@Component
public class ListenerDeTransacao {

    @KafkaListener(topics = "${spring.kafka.topic.transactions}")
    public void ouvir(EventoDeTransacao eventoDeTransacao) {
        System.out.println(eventoDeTransacao);
    }

}
```

No código acima a gente definiu nosso listener para isso é preciso seguir algumas etapas:

Primeiro a gente precisou configurar a anotação `KafkaListener` no qual é necessário configurar qual tópico ele irá 
coletar os eventos, como por exemplo, `${spring.kafka.topic.transactions}`!

O interessante que a gente utilizou o fator III. Configurações, na qual diz que você deve armazenar as configurações no 
ambiente, do `The Twelve-Factor App`, quer saber mais? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/twelve-factor-config.md)

Segundo a gente precisou adicionar qual evento a gente iria receber e para isso basta passar como parâmetro toda "mágica" 
de como tratar o evento foi definido na classe `KafkaConfiguration`!

Demais né!? Agora sabemos como consumir eventos no kafka!

## Informações de suporte

Quer saber mais sobre o Apache Kafka? Acesse o [link!](https://kafka.apache.org)

Quer saber mais sobre os modelos de entrega no Apache Kafka, acesse o [link!](https://kafka.apache.org/documentation/#semantics)

Quer saber mais sobre Consumidor? Acesse o [link!](https://kafka.apache.org/documentation/#theconsumer)
