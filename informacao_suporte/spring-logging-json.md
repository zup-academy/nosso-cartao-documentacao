# Como logar em formato JSON no Spring?

Vimos no material de [logging](../informacao_suporte/spring-logging.md) a importância de se logar!

Você sabia que com base nos logs, podemos utilizar ferramentas para indexar os mesmos e tomar decisões?

Essas ferramentas de coleta de logs (Logstash, Fluentd, Fluent bit) geralmente trabalham melhor com a indexação no formato 
[JSON](https://www.json.org/json-en.html)!

Demais né! Vamos fazer isso utilizando o Spring?

Primeiro, precisamos adicionar algumas configurações no nosso `pom.xml`, conforme abaixo:

Precisamos adicionar a seguinte propriedade:

```xml
<properties>
    <!-- Omitidas outras propriedades -->
    <ch.qos.logback.version>1.2.3</ch.qos.logback.version>
</properties>
```

Agora que adicionamos as propriedades, precisamos adicionar um gerenciador de dependência, conforme abaixo:

```xml
<dependencyManagement>

    <dependencies>
        <!-- Omitidas outras dependências -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-core</artifactId>
            <version>${ch.qos.logback.version}</version>
        </dependency>

        <dependency>

            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>${ch.qos.logback.version}</version>
        </dependency>

        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-access</artifactId>
            <version>${ch.qos.logback.version}</version>
        </dependency>

    </dependencies>

</dependencyManagement>
```

Gostaria de saber mais sobre Dependency Management no Maven? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)

Agora que está tudo configurado (Propriedades e Dependency Management), precisamos adicionar a seguinte dependência:

```xml
<dependencies>

    <dependency>
      <groupId>net.logstash.logback</groupId>
      <artifactId>logstash-logback-encoder</artifactId>
      <version>6.4</version>
    </dependency>

</dependencies>
```

Você deve estar pensando, está tudo configurado? Infelizmente falta apenas uma configuração!

Agora que está tudo configurado, precisamos adicionar o seguinte arquivo `logback-spring.xml` na pasta `/src/main/resources/`

**logback-spring.xml**

```xml
<configuration>

  <appender name="consoleAppender" class="ch.qos.logback.core.ConsoleAppender">
    <encoder class="net.logstash.logback.encoder.LoggingEventCompositeJsonEncoder">
      <providers>
        <timestamp/>
        <version/>
        <loggerName/>
        <threadName/>
        <logLevel/>
        <mdc/>
        <message/>
        <stackTrace/>
      </providers>
    </encoder>
  </appender>

  <logger name="jsonLogger" additivity="false" level="DEBUG">
    <appender-ref ref="consoleAppender"/>
  </logger>

  <root level="INFO">
    <appender-ref ref="consoleAppender"/>
  </root>

</configuration>
```

Pronto! Agora sim está tudo configurado! Vamos testar?

Para testar inicie sua aplicação conforme desejar ou utilizando o comando `mvn clean spring-boot:run` e verifique se 
os logs estão sendo escritos no formato [JSON](https://www.json.org/json-en.html)!

Um ponto importante! Além do log ser no formato [JSON](https://www.json.org/json-en.html), nossa aplicação precisa logar 
no **Stdout** do nosso sistema, pois, é o lugar que os coletores de logs ficam esperando os mesmos para serem processados 
e também não precisamos que nossa aplicação tenha a responsabilidade de escrever em um determinado arquivo e gerir o roteamento 
do mesmo!

Demais né!? Você sabia que foi aplicado um dos fatores do The Twelve Factor App?

Você aplicou o fator XI. Logs, na qual diz que devemos tratar logs como fluxos de eventos!

Quer saber mais? Acesse o [link!](../informacao_procedural/twelve-factor-logs.md)

## Informação de Suporte

Quer saber mais sobre logs? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-logging)

Quer saber mais sobre coletores de logs? Acesse o [link!](https://opensource.com/article/18/9/open-source-log-aggregation-tools)
