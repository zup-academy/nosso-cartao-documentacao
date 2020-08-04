# Criando Web Services Clients com Feign

Precisamos com certa frequência criar diferentes web service clients, nosso serviço,
na maioria das vezes necessitam se comunicar entre eles. 

Podemos encontrar alguns padrões no processo de criação desses clientes, envolvem
mapeamento de objetos de entrada, saída e configurações de URI como Path Params e Query Params.
O projeto OpenFeign pode nos ajudar nessa geração, já que podemos identificar um padrão na escrita 
desses clientes.

Para integrar o OpenFeign no ecossistema existe um projeto chamado Spring Cloud OpenFeign.
Então vamos ver como podemos usá-lo.

### Configurando a dependência do projeto

Nosso primeiro passo é incluir a dependência da biblioteca no nosso projeto

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```
Note que a dependência é do projeto "guarda-chuva" Spring Cloud



```java
@EnableFeignClients
``` 
Essa anotação indica para o Spring Framework que nosso projeto 



## Informações de suporte

- Me interessei pelo Feign, [aqui você encontra o código fonte e a documentação](https://github.com/OpenFeign/feign) 

- Quero saber os detalhes da ferramenta. [Aqui você encontra a documentação
completa](https://cloud.spring.io/spring-cloud-openfeign/reference/html/)