# Cronograma e plano de estudos e treinos

O nosso bootcamp tem duração de até 12 semanas. Preparamos toda uma sequência de estudos e treinos que visam te deixar preparado(a) para construir API's utilizando Java/Kotlin como linguagem e Spring/Micronaut + Hibernate como frameworks principais. Fazendo com que você possa focar no que mais importa, que é entregar valor para o cliente final usando tecnologia como meio. 

## O que vamos estudar e treinar?

Para que você se sinta e realmente seja capaz de construir API's, durante o bootcamp, você vai estudar e treinar em cima dos seguinte tópicos:

* Design de código orientado a objetos com a linguagem Java;
* Design de código orientado a objetos com a linguagem Kotlin;
* Testes automatizados de unidade para aumentar a confiabilidade de execução do software;
* JUnit para facilitar a escrita de testes automatizados;
* Mockito para ajudar na simulação de invocação a sistemas externos;
* SQL básico para realizar as operações de leitura e escrita necessárias;
* Spring Boot para facilitar a utilização de tecnologias do ecossistemas Spring;
* Spring MVC para facilitar na criação da camada web da aplicação;
* Spring Validation para facilitar no processo de validação da entrada dos dados;
* Spring Actuator para expor informações sobre a saúde da aplicação;
* Spring Scheduling para criar agendamentos;
* Spring Security para criar mecanismos de autenticação;
* Módulo de integração com o Feign do Spring;
* Hibernate para fazer o mapeamento entre o mundo orientado a objetos e relacional;
* Kafka para ser usado meio de integração assíncrona via mensageria;
* Open Tracing para conseguir seguir o fluxo de uma requisição em um sistema distribuído;
* Docker e Kubernetes para auxiliar no processo de criação de ambientes simulando a produção e deploy;
* Micronaut para construção API's ainda mais preparadas para o mundo Cloud Native.
* Stack de CI/CD da Amazon para que consiga fazer com que seu código seja um bom cliente da operação. Vamos de cultura DevOps. 

## Sua sequência de atividades considerando todas as 12 semanas

Primeiro começamos entendendo a estrutura do bootcamp e como ficar melhor
preparado(a) para consumir tudo que preparamos. Essa aqui é uma fase curta, porém fundamental. **Esta é a fase um do nosso bootcamp.**

* [Consumir o material sobre como ficar preparado(a) para o bootcamp](fique-preparado(a)-desafios/readme.md). Lá você vai entender direitinho como preparamos a jornada para você. 
* [Consumir o material sobre como ser um(a) melhor estudante](seja-um(a)-melhor-estudante/readme.md). Aqui você vai ter alguns vídeos que vão te ajudar a ser um(a) melhor estudante durante as 16 semanas.

Agora você vai fazer uma imersão de teoria sobre desenvolvimento web utilizando o paradigma de programação orientado a objetos com Java, Spring e Hibernate. Aqui é uma fase com muita teoria e alguns exercícios de fixação. Não se preocupe se sentir a cabeça ficar pesada, é uma sensação normal. Toda essa fase de teoria está centrada em cursos prontos da plataforma Alura. Você deve ter acesso para conseguir fazê-los. **Esta é a fase dois do nosso bootcamp**. 

Sugerimos fortemente que você assista os videos entre 1.5 e 2x de velocidade. Lembre que a ideia é que você tenha contato e que tenha um primeiro conhecimento sobre isso tudo. Depois vai chegar a parte do treino em cima dessas teorias e aí esperamos que você fique ainda mais capaz de utilizar as teorias de maneira mais fluida.  

* [Java Servlet: Fundamentos da programação web Java](https://www.alura.com.br/curso-online-servlets-fundamentos-programacao-web-java);
* [HTTP: Entendendo a web por baixo dos panos](https://www.alura.com.br/curso-online-http-fundamentos);
* [SQL até Consultas SQL: Avançando no SQL com MySQL](https://www.alura.com.br/formacao-oracle-mysql). São os dois primeiros cursos;
* [JPA e Hibernate](https://www.alura.com.br/curso-online-jpa-hibernate-persistencia-objetos);
* [Spring Boot 1](https://www.alura.com.br/curso-online-spring-boot-api-rest);
* [Spring Boot 2](https://www.alura.com.br/curso-online-spring-boot-seguranca-cache-monitoramento);
* [Spring Boot 3](https://www.alura.com.br/curso-online-spring-boot-profiles-testes-deploy);
* [Spring Data Jpa](https://www.alura.com.br/curso-online-spring-data-jpa);
* [SOLID](https://www.alura.com.br/curso-online-orientacao-a-objetos-avancada-e-principios-solid);

Agora que você passou por uma fase intensa de teoria, chegou a hora de treinar muito. Você vai construir dois projetos do zero. Nessa fase é importante que você vá se analisando e prestando muita atenção em relação ao nível de facilidade de cada funcionalidade construída. **Tem que ir ficando mais fácil**. Se não estiver ficando fácil, fique alerta, talvez você precise de ajuda. **Agora você entra na fase três do nosso bootcamp.**

* [Implementar o desafio de construção de uma API que simule a editora Casa do Código](./treino-casa-do-codigo);

O desafio de implementação da Casa do Código foi muito importante para que você treinasse sua habilidade em desenvolver API's web. O próximo desafio exige habilidades bem similares, o que é bom. Lembre que a repetição em cenários variados eleva seu nível. Só que agora, além de ser um desafio mais complexo, também vai exigir de você a criação de testes automatizados. 

Para te deixar ainda mais preparado(a), temos alguns conteúdos sobre testes.
 
 * [Introdução a testes automatizados](https://www.alura.com.br/curso-online-tdd);
 * [Testes de integração](https://www.alura.com.br/curso-online-teste-de-integracao);
 * [Conteúdo mais profundo sobre testes](/testes-automatizados-reveladores-de-bugs). 

Agora, com um pouco mais de teoria sobre como os testes podem ajudar no aumento de confiabilidade de execução do código, mergulhe no desafio de criar uma API que simula parte do Mercado Livre.

* [Implementar o desafio de construção de uma API que simule parte do funcionamento do mercado livre](./treino-mercado-livre);

Neste ponto da jornada, você deve estar se sentindo mais confiante e mais capaz de construir API's com as tecnologias e práticas até aqui trabalhadas. Vamos para o desafio final. Que é construir uma API que simule o funcionamento do credicard zero, um produto do Itaú. **Esta é a fase quatro do nosso bootcamp.**

Vamos começar pela teoria que vai ser praticada no primeiro microservice, o de criação de propostas.

* [Introdução a Docker](https://www.alura.com.br/curso-online-docker-e-docker-compose);
* [Healthcheck](informacao_procedural/healthcheck.md);
* [Readiness checks](informacao_procedural/readiness_checks.md);
* [Spring Actuator](informacao_suporte/spring-actuator.md);
* [Spring Health check](informacao_suporte/spring-health-check.md);
* [Seguraça em ambientes cloud native](informacao_procedural/seguranca_cloud_native.md);
* [Introudção a Oauth](informacao_suporte/oauth*md);
* [Introdução a Keycloak](informacao_suporte/keycloak.md);
* [Sobre métricas](informacao_procedural/metric.md);
* [Métricas tipo RED](informacao_procedural/metric-red.md);
* [Métricas tipo USE](informacao_procedural/metric-use.md);
* [Introdução ao Prometheus](informacao_procedural/prometheus.md);
* [Spring Actuator e métricas](informacao_suporte/spring-actuator-metrics.md)
* [Introdução a Open tracing](informacao_procedural/open-tracing.md);
* [Jaeger como implementaçãod de Open tracing](informacao_suporte/jaeger.md);

Agora que você fez mais imersão teórica, vamos treinar! Nele você vai utilizar tudo que você estudou e até um pouco mais!

* [Implemente o microservice relativo a criação de propostas](proposta/)

Com o microservice de propostas implementado, chegou a hora de implementar um novo serviço, o que cuida das transações do cartã de crédito. Como é de praxe, antes de começar, vamos primeiro estudar a teoria necessária. 

* [Introdução a Apache Kafka](https://www.alura.com.br/curso-online-kafka-introducao-a-streams-em-microservicos);

Chegou a hora de programar o serviço de transação. Ele é um serviço pequeno, mas vai te desafiar a utilizar o Kafka integrado com o Spring e te deixar ainda mais preparado(a) para utilizar essa forma de integração.

* [Serviço de transação](transacao/);

Nesse momento do nosso bootcamp, você já deve estar se sentindo mais 
apto(a) a criar API's REST que possam ser deployadas em ambientes Cloud Native. Agora vamos para a fase final, onde vamos nos desafiar a transferir todo esse conhecimento para uma nova stack de tecnologias, a Orange Stack!  Antes de mais nada, deixe a gente te contar um pouco sobre essa nova stack. 

A Zup + Itaú decidiram apostar em uma nova para facilitar que você possa focar ainda mais nas funcionalidades e potencializar negócios. A Orange Stack vai atuar em diversas vertentes do desenvolvimento, tais como:

* Backend;
* Frontend;
* Pipeline de Continuos Integration(CI) e Continuos Deployment(CD);
* Múltiplas áreas relativas a Data Science;

Aqui no nosso programa, vamos focar nas tecnologias associadas com a vertente de backend. Entre essas tecnologias temos:

* Kotlin;
* Micronaut;
* GRPC;
* JUnit;
* Pitest;
* Prometheus;
* Jaeger;
* Gradle;
* Redis;
* Amazon EKS;
* AWS Secret Manager;
* Gitlab;
* AWS Code Pipeline;
* AWS Code Build;
* AWS Code Deploy;

Algumas delas, como JUnit, Prometheus e Jaeger já trabalhamos. Vamos continuar fazendo uso delas e estudar e praticar em cima de mais algumas agora:

* Kotlin;
* Micronaut;
* GRPC;
* Gradle;
* AWS EKS;
* AWS Secret Manager;
* Gitlab;
* AWS Code Pipeline;
* AWS Code Build;
* AWS Code Deploy;

Está pronto(a)? Vamos para a **fase cinco do nosso programa**. 

ESTAMOS NESSE MOMENTO CONSTRUINDO O MATERIAL DA FASE 5 PARA QUE VOCÊ POSSA SE DESAFIAR AINDA MAIS, AGUARDE POR ATUALIZAÇÕES AQUI :). 

## Cronograma para executar todas as atividades

Nosso programa está estimado em 12 semanas e abaixo temos o cronograma. Lembre também que temos toda uma equipe pronta para te dar suporte, tirar dúvidas e te direcionar.

1. Estimamos que você conclua a **fase 1** + **fase 2** até a segunda semana. Essa é uma fase muito focada em teoria e atividades de fixação
2. Estimamos que você conclua a **fase 3** até a quarta semana.
3. Estimamos que você conclua a **fase 4** até a sétima semana.
3. Agora você tem até 5 semanas para fechar a **fase cinco** !

O nosso programa é intenso e exige muito esforço da sua parte. Esperamos contar com toda sua energia!

## Lembrete final

Assim como um jogo de video game, aqui você também precisa passar fase por fase. Se uma fase parecer fácil para você, não tem problema, passa por ela mais rápido :). 


