# Acessando Grafana pela primeira vez!!!!

O Grafana é uma ferramenta bastante importante em um ambiente de aplicações distribuídas, ele nos ajuda a mostrar
nossas métricas de uma maneira mais organizada e simples de visualizar.

Para nosso uso vamos _"subir"_ uma instância para que possamos criar nossos gráficos bonitões. Vale a pena notar
que estamos rodando em ambiente de desenvolvimento, quando estamos em ambiente produtivo precisamos de provavelmente
mais de uma instância para garantir alta disponibilidade e resiliência. Isso é muito importante!!!!

Se você usou nosso [docker compose](../ops/docker-compose.yaml) você poderá verificar
que temos um elemento chamado **grafana**. Abaixo segue o fragmento

```yaml
    ##
    ## restante omitido
    ##
  grafana:
    image: grafana/grafana
    volumes:
      - grafana-volume:/var/lib/grafana
      - ./grafana/:/etc/grafana/provisioning/
    ports:
      - 3000:3000
    ##
    ## restante omitido
    ##
```

Temos algumas configurações de volumes que serão utilizadas para configuração
da ferramenta, mas não é importante para esse momento.

Neste momento atente-se à porta que está mapeada para [localhost:3000](http://localhost:3000/) então vamos nos conectar
na aplicação!!!

No primeiro acesso você será redirecionado para a tela de login, e na primeira execução do grafana você terá que usar
o seguinte usuário

usuario: **admin**

senha: **admin**

Logo depois você será questionado sobre trocar a sua senha faça isso com cuidado, essa senha será utilizada nas suas próximas
tentativas.

Vamos ver a tela de login

![login grafana](../images/grafana_login.png " login grafana")

Como falamos anteriormente o **Grafana** é uma ferramenta de _Criação e Visualização de Gráficos_, então ele não tem nenhum dado incluído na ferramenta
logo, precisamos configurar nossa fonte de informação de dados e imagina qual seria nossa fonte de informação??? Nosso **prometheus**

Mas antes, podemos explorar a home do grafana, importante notar que os menus do Grafana, na versão que estamos utilizando
são localizados do lado superior esquerdo.

Aqui você pode navegar nos seus dashboards, realizar configurações do grafana, configurar usuários
entre outras opções.

Vamos ver isso na figura abaixo!!!

![menus grafana](../images/menus_grafana.png  "menus grafana")

Pronto!!! Esse foi nosso primeiro acesso ao grafana, uma ferramentas bastante poderosa na criação e configuração 
de gráficos.

Explore a ferramenta, neste próximo passa vamos mostrar como podemos configurar nossa fonte
de informação, se você navegou pela ferramenta.Vamos lá!!!

# Informações de suporte

* Quer saber mais sobre Prometheus? Acesse o [link!](https://prometheus.io/)
