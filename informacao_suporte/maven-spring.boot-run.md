# Rodando nossa aplicação com maven!!!

Durante a fase de desenvolvimento existe uma maneira bem legal de rodar nossa aplicação usando o próprio maven.

Esse processo é bastante simples e utiliza o modelo de plugins do maven.

Nosso primeiro passo é garantir que nossa aplicação esta configurada com o plugin do spring boot. 

Verifique se no pom.xml do seu projeto o plugin do spring boot está configurado

```xml
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
``` 


Bom, se seu projeto já está configurado com isso agora podemos rodar nossa aplicação.

Para isso execute o seguinte comando

```shell script
mvn spring-boot:run
```

Pronto!!! Agora você pode esperar sua aplicação subir...   

# Informação de Suporte

* Talvez você possa estar se perguntando o que é o maven??? [Este link pode esclarecer algumas coisas para você](https://maven.apache.org/)

* Maven eu tenho uma idéia, mas o que são plugins do maven. [Este link tem o detalhamento necessário](https://maven.apache.org/plugins/index.html)

* Mas, se você quer entender tudo do plugin do spring boot para o maven. A documentação completa pode ser [encontrada aqui](https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/html/)  

* Quais são as opções de comando que eu posso executar com o plugin do spring boot. [Aqui estão elas](https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/html/#goals)


# Dicas Claudio

* Essa não é a melhor maneira de rodar suas aplicações em ambiente produtivo, tenha em mente que essa maneira ś recomendada somente durante o ciclo de
desenvolvimento