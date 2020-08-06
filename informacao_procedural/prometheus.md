# Prometheus

O Prometheus é um sistema de monitoramento de código aberto baseado em métricas. Claro, Prometheus está longe de ser o 
único lá fora, então o que o torna notável?

Prometheus faz uma coisa e faz bem. Ele possui um modelo de dados simples, porém poderoso, e uma linguagem de consulta 
que permite analisar o desempenho de seus aplicativos e infraestrutura. Ele não tenta resolver problemas fora do espaço 
das métricas, deixando-os para outras ferramentas mais apropriadas.

O mesmo é escrito principalmente em Go e licenciado sob a licença Apache 2.0, na qual existem centenas de pessoas que 
contribuíram para o projeto em si, que não são controladas por nenhuma empresa.

Demais né! Um projeto focado em métrica, código aberto e sem nenhuma empresa por traz, esses fatores o deixam muito 
poderoso e fica claro sua utilização no mercado, principalmente na Zup!

E ainda mais, para instrumentar seu próprio código, existem bibliotecas em todas as linguagens populares, incluindo Go, 
Java, C#, Python, Ruby, Node.js, etc. Softwares como Kubernetes e Docker já estão instrumentados com as bibliotecas do 
Prometheus. Para softwares de terceiros que expõe métricas em algum outro formato que não seja do Prometheus, existem 
centenas de integrações disponíveis. Eles são chamados de exportadores e incluem HAProxy, MySQL, PostgreSQL, Redis, 
JMX, SNMP, Consul e Kafka.

## Funcionalidades

* PromQL, uma linguagem de consulta flexível para efetuar consultas.
* Coleta de métricas ocorre por meio de um modelo pull sobre HTTP.
* Receber métricas é suportado através de um gateway intermediário.

## Coleta de métricas

Existem dois modelos de coleta de métricas:

- Pull model
- Push model

#### Pull model

O modelo pull model é o mais utilizado pelo mercado, pois o Prometheus tem a responsabilidade de coletar as métricas de 
acordo com os endereços configurados em seu arquivo de configuração, ou seja, se você configurou para ele coletar as métricas 
do endereço `www.prd-servico-proposta.com.br/actuator/prometheus` a cada 5s o mesmo fará!

Esse modelo é muito bom, pois a sua aplicação não tem a responsabilidade de enviar as métricas e sim de apenas fornecer 
no formato Prometheus e certamente o mesmo (Prometheus) irá coletar!

Demais né! Conhecia esse modelo?

#### Push Model

O modelo push model é o menos utilizado, pois ele atende um cenário muito específico, como por exemplos operações de 
curta duração, como uma Tarefa, Função(Serverless), etc.

Como essas operações duram pouco, seus endereços mudam bastante e fica inviável do Prometheus gerenciar isso, portanto a 
responsabilidade de enviar as métricas são da aplicação (operação de curta duração).

Para atender esse cenário o Prometheus provê uma API para receber essas métricas!

Demais né! Lembrando é apenas para casos de operações com curta duração! Se você utiliza uma aplicação que roda horas, 
dias, meses, etc. Utilize o modelo de pull model e remova a complexidade da sua aplicação!

Quer saber mais sobre Push Model e quando utilizar? O Prometheus tem uma [página](https://prometheus.io/docs/practices/pushing/) sobre isso!

# Dicas de Luram Archanjo

Prometheus é muito utilizado no mercado e recomendado a sua utilização dentro da Zup, portanto, tente se aprofundar ao 
máximo sobre o tema em sua área de atuação!

Aprenda sobre as melhores práticas de métricas! [Aqui você encontra como fazer isso!](https://prometheus.io/docs/practices/naming/)

Aprenda sobre alertas, pode te ajudar muito quando estiver com alguma aplicação em Produção! [Aqui você encontra como fazer isso!](https://prometheus.io/docs/alerting/latest/overview/)

# Informações de suporte

Quer saber mais sobre Prometheus? Acesse o [link!](https://prometheus.io/)