# Como configurar o Spring Boot Actuator?

O Spring Boot Actuator inclui vários recursos adicionais para ajudá-lo a monitorar e gerenciar seu aplicativo quando você o envia à produção, como por exemplo:
Endpoint para monitoramento da saúde da aplicação (Health Check).

Endpoint para expor métricas da aplicação.

Endpoint para expor as propriedades da sua aplicação.

Super legal né! Quer saber quais são os outros endpoints, acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-endpoints)

Vamos configurar!?

1º Precisamos adicionar a seguinte dependência em seu arquivo `pom.xml`:

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-actuator</artifactId>
	</dependency>
</dependencies>
```

2º Precisamos verificar se está tudo configurado, para isso abra em seu navegador o seguinte endereço:

`http://localhost:8080/actuator`

Neste endpoint irá listar todos os endpoints configurados, como por exemplo:

```
# Endpoint para monitoramento da saúde da aplicação (Health Check)

http://localhost:8080/actuator/health
```

Eba! Está tudo OK!

Sim, mas antes de continuar com sua tarefa, aconselhamos dar uma lida no tópico abaixo, sobre segurança!

## Dicas

Não deixe pública sua API, alinhe sempre com sua equipe as melhores práticas, como por exemplo:

- Adicionar autenticação
- Adicionar autorização
- Não negligencie as informações que você está expondo sobre a sua infraestrutura.

## Informação de Suporte

Talvez você esteja pensando sobre segurança no Spring Boot Actuator... [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_suporte/spring-actuator-security.md)

Quer saber mais sobre Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-enabling)

Quer saber mais sobre o The Twelve-Factor App? Acesse o [link!](https://12factor.net/pt_br/)
