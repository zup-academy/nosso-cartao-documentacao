# Kafka - Tópico

Na arquitetura do Apache Kafka existem vários componentes, como por exemplo, o Tópico que tem a responsabilidade de 
representar um stream de evento, como por exemplo, um tópico de transações!

Uma analogia para a gente entender o que é um Tópico é dizer que o mesmo é uma tabela no banco de dados, onde contém 
todos os registros e a ordem de cadastro dos mesmos!

Portanto, caso um determinado consumidor queira consumir as transações, basta o mesmo se conectar e começar operar 
no Tópico.

Demais né!?

O Tópico no Apache Kafka tem uma característica bastante importante, a partição, no qual permite ser distribuído 
em vários brokers do Kafka via `Replication Factor`, conforme imagem abaixo:

![alt text](../images/kafka-001.png "Apache Kafka")

Quer saber mais sobre partição? [Aqui tem uma explicação do que entendemos que você deve considerar!!](../informacao_suporte/kafka-partition.md)

## Informações de suporte

Quer saber mais sobre o Apache Kafka? Acesse o [link!](https://kafka.apache.org)

Quer saber mais sobre Tópico? Acesse o [link!](https://kafka.apache.org/)

Quer saber mais sobre Persistência? Acesse o [link!](https://kafka.apache.org/documentation/#persistence)

Quer saber mais sobre Replicação? Acesse o [link!](https://kafka.apache.org/documentation/#replication)