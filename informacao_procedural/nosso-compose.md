# Docker Compose Cartão Branco

A solução do Cartão Branco se utiliza de vários serviços adjacentes aos nossos serviços de Proposta,
Transação e Fatura.

Esses serviços podem ser utilizados para coletar métricas, coletar tracings, banco de dados e 
IAM. 

Perceba que para esses serviços somos apenas **"consumidores"**, não vamos codificar nenhuma alteração neles.

Vamos ver na prática como esse arquivo está configurado

```yaml
version: '3.6'
services:

  zookeeper:
    image: "confluentinc/cp-zookeeper:5.2.1"
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
      ZOOKEEPER_SYNC_LIMIT: 2

  kafka:
    image: "confluentinc/cp-kafka:5.2.1"
    ports:
      - 9092:9092
    depends_on:
      - zookeeper
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: "zookeeper:2181"
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:29092,PLAINTEXT_HOST://localhost:9092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: "1"
      KAFKA_AUTO_CREATE_TOPICS_ENABLE: "true"

  postgres:
    image: 'postgres:alpine'
    volumes:
      - postgres-volume:/var/lib/postgresql/data
    restart: 'always'
    ports:
      - 5432:5432
    environment:
      POSTGRES_USER: keycloak
      POSTGRES_PASSWORD: password
      POSTGRES_DB: keycloak
      POSTGRES_HOST: postgres

  keycloak:
    image: jboss/keycloak
    ports:
      - 18443:8443
      - 18080:8080
      - 19990:9990
    depends_on:
      # Just a delay to wait for postgres! This is not recommended!
      - grafana
      - prometheus
      - jaeger
      - kafka
      - zookeeper
      - contas
      - analise
      - transacoes
      - postgres
    environment:
      DB_VENDOR: postgres
      DB_ADDR: postgres
      DB_PORT: 5432
      DB_DATABASE: keycloak
      DB_USER: keycloak
      DB_PASSWORD: password
      KEYCLOAK_USER: admin
      KEYCLOAK_PASSWORD: Pa55w0rd
      POSTGRES_PORT_5432_TCP_ADDR: 127.0.0.1

  analise:
    image: 'zupacademy/analise-financeira'
    restart: 'always'
    ports:
      - 9999:9999
    environment:
      SERVER_PORT: 9999
      LOG_LEVEL: INFO
      URL_SISTEMA_CARTAO: http://contas:8888/api/cartoes

  contas:
    image: 'zupacademy/contas'
    restart: 'always'
    ports:
      - 8888:8888
    environment:
      SERVER_PORT: 8888
      LOG_LEVEL: INFO

  transacoes:
    image: 'zupacademy/transacoes'
    restart: 'always'
    ports:
      - 7777:7777
    depends_on:
      - kafka
    environment:
      SERVER_PORT: 7777
      LOG_LEVEL: INFO
      KAFKA_HOST: "kafka:29092"

  jaeger:
    image: jaegertracing/all-in-one
    restart: always
    ports:
      - 5775:5775/udp
      - 6831:6831/udp
      - 6832:6832/udp
      - 5778:5778
      - 16686:16686
      - 14268:14268
      - 14250:14250
      - 9411:9411
    environment:
      COLLECTOR_ZIPKIN_HTTP_PORT: 9411

  prometheus:
    image: prom/prometheus
    volumes:
     - ./prometheus.yml:/etc/prometheus/prometheus.yml
     - prometheus-volume:/etc/prometheus/
    ports:
      - 9090:9090
    depends_on:
      - analise
      - contas
      - transacoes

  grafana:
    image: grafana/grafana
    volumes:
      - grafana-volume:/var/lib/grafana
      - ./grafana/:/etc/grafana/provisioning/
    ports:
      - 3000:3000
    depends_on:
      - prometheus

volumes:
  grafana-volume:
  prometheus-volume:
  postgres-volume:
```

Perceba que cada elemento do yaml é um elemento na infra-estrutura, temos alguns exemplo como kafka,
grafana, prometheus e outros.

Cada elemento pode ser encontrado na rede interna do compose pelo nome. Por exemplo: o **grafana** em algum 
momento precisa se conectar com o **prometheus**, e quando ele chamar por **prometheus** ele é capaz 
de encontrar o container do **prometheus** na rede. Um comportamento similar a hostnames 

## Informações de suporte

* Talvez você pode estar se perguntando, qual a função sobre o docker-compose. [Aqui você pode encontrar](https://docs.docker.com/compose/)
  * Se você está curioso, e que entender um pouco mais sobre a criação de um compose file. [Este link é uma ótima fonte para isso](https://docs.docker.com/compose/gettingstarted/)
  * Ou ainda você quer algumas dicas de como criar imagens para ambiente de desenvolvimento. [Aqui você pode encontrar
  algumas dicas de como fazer isso de maneira eficiente](https://docs.docker.com/develop/dev-best-practices/)
  * Mas se você se interessou pelo arquivo do compose e gostaria de explorar mais. [Você pode encontrar na documentação
  a referência](https://docs.docker.com/compose/compose-file/).
  * Um ponto importante, é que existe uma matriz de compatibilidade entre docker e docker-compose. Muito cuidado com
  esse detalhe isso pode causar um funcionamento inadequado. [Aqui você pode encontrar este link](https://docs.docker.com/compose/compose-file/compose-versioning/)
  * Mas se você sentiu a falta de um conteúdo mais prático. [Aqui você pode aprender como rodar algumas aplicações](https://www.alura.com.br/artigos/compondo-uma-aplicacao-com-o-docker-compose)
* Talvez você se interesse por redes em containers. Então aqui temos alguns links úteis  
    * Se você interessou-se pelo comportamento de redes nos containers. [Esse link explica
    detalhes do funcionamento de redes](https://docs.docker.com/config/containers/container-networking/)
    * Talvez você pode se perguntar qual é o modelo padrão de rede no docker. [Este link explica um pouco do modelo bridge](https://docs.docker.com/network/bridge/)    
    * Ou ainda pode ter alguma dúvida sobre a existência de outros modelos de rede no docker. [Sim, temos um modelo chamado overlay, aqui você acha detalhes sobre ele](https://docs.docker.com/network/overlay/) 
* Ou ainda voc    
    