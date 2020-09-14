# Como configurar minha aplicação no Prometheus?

Para configurar sua aplicação no Prometheus, primeiro precisamos entender o que é **Target**!

> Está em dúvida sobre o que é Target no Prometheus? Não se preocupe! Escrevemos um [material específico para você!](../informacao_procedural/acessando_prometheus.md)

Eba! Agora que sabemos o que é Prometheus e Target! Vamos colocar configurar nossa aplicação?

Imagino que esteja utilizando nosso [docker-compose](../ops/docker-compose.yaml), primeiro precisamos parar o container 
do Prometheus para isso execute o comando abaixo:

```shell script
$ echo "Syntax"
$ docker-compose -f <DOCKER-COMPOSE-FILE>.yaml stop <NOME-DO-SERVIÇO>

$ echo "Exemplo"
$ docker-compose -f nosso_cartao.yaml stop prometheus
```

Agora que nosso container do Prometheus está parado, precisamos criar e configurar o arquivo `prometheus.yml` na pasta 
raiz onde se encontra o arquivo do nosso docker-compose, como por exemplo o `nosso_cartao.yaml`!

Caso já exista o arquivo `prometheus.yml`, utilize o mesmo e adicione o `job_name` no ramo `scrape_configs` conforme 
exemplo abaixo:

```yaml
# Restante omitido
scrape_configs:

  - job_name: 'proposta'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['localhost:8080']
```

Caso não tenha o arquivo `prometheus.yml` crie o mesmo e adicione as seguintes informações:

```yaml
global:
  scrape_interval:     15s
  evaluation_interval: 15s

scrape_configs:

  - job_name: 'proposta'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['localhost:8080']
```

Agora que o arquivo `prometheus.yml` foi criado e configurado, precisamos mapear o mesmo no nosso [docker-compose](../ops/docker-compose.yaml), 
na seção do Prometheus, conforme exemplo abaixo:

```yaml
# Restante omitido

prometheus:
    image: prom/prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus-volume:/etc/prometheus/
    network_mode: host
    expose:
      - 9090

# Restante omitido
```

Eba está tudo configurado! Vamos testar?

Para testar precisamos somente iniciar o container novamente, conforme exemplo abaixo:

```shell script
$ echo "Syntax"
$ docker-compose -f <DOCKER-COMPOSE-FILE>.yaml start <NOME-DO-SERVIÇO>

$ echo "Exemplo"
$ docker-compose -f nosso_cartao.yaml start prometheus
```

Após iniciar o Prometheus vá no aba de [Targets](http://localhost:9090/targets) e verifique se sua aplicação está UP!

## Informações de suporte

Gostaria de saber mais sobre Prometheus? Acesse o [link!](../informacao_procedural/prometheus.md)

Gostaria de saber mais sobre o arquivo `prometheus.yml`? Acesse o [link!](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#configuration-file)