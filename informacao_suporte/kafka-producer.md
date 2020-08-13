# Kafka - Produtor

Na arquitetura do Apache Kafka existem vários componentes, como por exemplo, o **Produtor** que tem a responsabilidade 
de enviar os eventos de um determinado tópico.

O produtor envia os eventos para o broker líder, ou seja, em um conjunto de máquinas (brokers) que formam o cluster Kafka, 
é eleito um líder que irá receber os eventos de acordo com o tópico e partição! Portanto, no Apache Kafka não existe um 
líder geral e sim um líder específico por partição.
 
Para que seja possível saber os líderes o Apache Kafka informa para os produtores quais brokers estão aptos a receber 
eventos, por isso, é de extrema importância ter replicações das partições, pois, se uma máquina (broker) cai a outra 
assume a liderança da(s) partição(ões)!

Demais né!?

Para enviar um evento é preciso enviar as seguintes informações:

- Nome do tópico.
- Corpo do evento, geralmente enviado no formato JSON.
- Chave (Opcional), caso deseje que todas as mensagens sejam enviadas para uma mesma partição e de forma ordenada.

Eba! Sabemos como funciona um produtor!

Calma! Vamos aprender sobre o ciclo de vida do mesmo?

Sabia que é possível configura retry para que não percamos mensagens?

![alt text](../images/kafka-009.png "Apache Kafka")

Demais né!

Além do ciclo de vida do retry, existe a possibilidade de configurar o modelo de reconhecimento do envio do evento?

Isso pode ser muito útil para a gente garantir de fato que o evento foi replicado, etc!

Para que isso seja possível o produtor deve informar qual modelo de reconhecimento ([acks](https://kafka.apache.org/documentation/#acks)) 
ele quer, como por exemplo:

- 0: O produtor não irá esperar pelo reconhecimento do recebimento do evento pelo Apache Kafka.
- 1: O produtor somente irá esperar pelo reconhecimento do recebimento do evento pelo líder.
- all: O produtor irá esperar pelo reconhecimento do recebimento do evento por todos os brokers que tenha a partição!

Demais né! Portanto, se deseja não perder mensagem utilize o modelo de reconhecimento do tipo `all`.

# Dicas de Luram Archanjo

É de extrema importância saber os modelos de reconhecimento de eventos, pois, isso impacta diretamente no negócio, como 
por exemplo, imagina que é um evento de transação bancária e por algum motivo foi perdido esse evento?

Impacta demais no negócio, portanto, leva-se sempre em consideração os seguintes pontos:

- Modelo de reconhecimento
- Quantidade de retry
- Idempotência

Quer saber mais sobre os modelos de entrega no Apache Kafka, acesse o [link!](https://kafka.apache.org/documentation/#semantics)

# Informações de suporte

Quer saber mais sobre o Apache Kafka? Acesse o [link!](https://kafka.apache.org)

Quer saber mais sobre os modelos de entrega no Apache Kafka, acesse o [link!](https://kafka.apache.org/documentation/#semantics)

Quer saber mais sobre Produtor? Acesse o [link!](https://kafka.apache.org/documentation/#theproducer)