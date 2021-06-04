# Kafka

Antes de falarmos de Kafka precisamos contextualizar o que é `Event streaming`!

Streaming de eventos é uma prática de capturar dados em tempo real de fontes de eventos como bancos de dados, sensores, 
dispositivos móveis e serviços, armazenando-os de forma duradoura para serem manipulados, processados em tempo 
real e também retrospectivamente.

Esses eventos podem ser direcionados para diferentes fontes, como por exemplo, sistema de análise, sistema de fraude, 
data lake, etc.
 
E para finalizar o streaming de eventos, também, garante um fluxo contínuo de dados para que as informações certas 
estejam no lugar certo, na hora certa.

Demais né? Qual a motivação de utilizar?

Imagina um banco! Não seria legal após a gente fazer uma compra no cartão de crédito e a mesma aparecer logo em seguida 
na fatura?

Hoje alguns bancos, tem que consolidar as transações, por isso leva-se algumas horas para aparecer na nossa fatura!

Imagina se tivesse um evento `ComprarEfetuda` no qual fosse publicado no `Event streaming` e o serviço de fatura 
processa-se segundos ou minutos depois!

A experiência do usuário mudaria muito, correto?

Visando isso, a comunidade criou o Apache Kafka no qual é uma plataforma de streaming de eventos distribuída 
de código aberto, usada por milhares de empresas para pipeline de dados de alto desempenho, análise de streaming, 
integração de dados e aplicativos de missão crítica.

O Apache Kafka tem algumas características interessantes, por exemplo:

- Alta disponibilidade
- Alta performance
- Escalabilidade 
- Modelo de entrega

Quando falamos de modelo de entrega, existem dois tipos:

- push model: os dados são enviados para os consumidores.
- pull model: os dados são coletados pelos consumidores.

O Apache Kafka optou pelo uso do pull model, pois, provê algumas vantagens bem interessantes, por exemplo:

- Consumidores conseguem controlar a quantidade de eventos que buscam, reduzindo as operações na rede.
- Consumidores conseguem controlar quais mensagens querem consumir, por exemplo, todas da última semana, ano, mês.
- Apache Kafka não precisa controlar os envios de eventos.

## Dicas

O Apache Kafka é muito utilizado pela **Zup** e outras empresas, portanto, aproveita para se aprofundar nesse assunto, como 
por exemplo?

- Por que ele é tão performático? Dê uma olhada no modelo [pull model](https://kafka.apache.org/documentation/#design_pull)
- Quais são seus casos de uso? Dê uma olhada no [link!](https://kafka.apache.org/uses)
- Como ele foi desenhado, quais são suas motivações? Dê uma olhada no [link!](https://kafka.apache.org/documentation/#design)

## Informações de suporte

Quer saber mais sobre Apache Kafka? Acesse o [link!](https://kafka.apache.org/)
