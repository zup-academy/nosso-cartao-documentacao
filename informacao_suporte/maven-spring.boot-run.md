# Rodando nossa aplicação com Maven!

Durante a fase de desenvolvimento existe uma maneira bem legal de rodar nossa aplicação usando o próprio Maven.

Esse processo é bastante simples e utiliza o modelo de plugins do Maven.

Nosso primeiro passo é garantir que nossa aplicação esteja configurada com o plugin do Spring Boot. 

Verifique se no `pom.xml` do seu projeto o plugin do Spring Boot está configurado.

```xml
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
``` 

Bom, se o seu projeto já está configurado com isso agora podemos rodar nossa aplicação.

Para isso execute o seguinte comando:

```shell script
mvn spring-boot:run
```

Pronto!!! Agora você pode esperar sua aplicação subir...   

# Informação de Suporte

* Talvez você possa estar se perguntando o que é o Maven??? [Este link pode esclarecer algumas coisas para você](https://maven.apache.org/)

* Maven eu tenho uma idéia, mas o que são plugins do Maven. [Este link tem o detalhamento necessário](https://maven.apache.org/plugins/index.html)

* Mas, se você quer entender tudo do plugin do Spring Boot para o Maven. A documentação completa pode ser [encontrada aqui](https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/html/)  

* Quais são as opções de comando que eu posso executar com o plugin do Spring Boot? [Aqui estão elas!](https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/html/#goals)

## Dicas de Claudio Eduardo Oliveira

* Essa não é a melhor maneira de rodar suas aplicações em ambiente produtivo, tenha em mente que essa maneira é 
recomendada somente durante o ciclo de desenvolvimento!