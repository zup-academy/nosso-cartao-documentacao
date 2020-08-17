# Importando gráficos Grafana

Já sabemos como realizar login e configurar um datastore no grafana, então agora
podemos ir para parte mais legal, que é ver os gráficos funcionando.

Então vamos lá!!!

Primeiro vamos localizar o menu do nosso canto superior direito, esse é o modelo
que o grafana está usando nas versões atuais.

Localize o menu import abaixo, como na figura abaixo

![import grafana](../images/import.png " import grafana")

Temos um dashboard pré-configurado com configurações de métricas padrão reportadas
pelo Spring Boot, você pode encontrar ele [aqui](../ops/grafana/spring-boot.json)

Copie o conteúdo do arquivo e cole no campo *Import via panel json*, como mostrado
na figura abaixo

![load grafana](../images/load_grafana.png " load grafana")

Então pressione o botão **Load**

No próximo passo você será redirecionado para configurar as opções do **Dashboard**, neste tela você pode
escolher um nome para seu Dashboard, folder que é uma estrutura de diretórios de gráficos
e o mais importante que é a fonte de seus dados.

Fizemos previamente a configuração de fonte de dados, mas se você não chegou nesse passo recomendamos
realizá-lo, [você pode aprender como fazer clicando aqui](configurando_datastore_grafana.md)

Escolha a fonte de dados e clique em **Import**

![import final grafana](../images/import_grafana_final.png " import final grafana")

Depois de clicar em **Import** você será redirecionado para seu dashboard como na figura abaixo!!!

![dashboard spring grafana](../images/dashboard_spring_grafana.png " dashboard spring grafana")

Massa!!! Perceba que muitas métricas já estão sendo usadas no gráfico. No Canto superior direito
já temos a métrica **Uptime** do nosso serviço de _Análise Financeira_. Perceba como
a utilização de uma ferramenta de gráficos nos ajudar de maneira bem rápida entender alguns
comportamentos do nosso sistema.

Logo abaixo da métrica de **Uptime** temos a utilização de **CPU** pelo nosso serviço de Análise. Note
que rapidamente conseguimos perceber que ele está operando sem nenhuma pressão, devido ao baixo consumo de 
CPU.

# Informações de suporte

* Quer saber mais sobre Prometheus? Acesse o [link!](https://prometheus.io/)
