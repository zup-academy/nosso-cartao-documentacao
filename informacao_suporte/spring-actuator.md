# Como configurar o Spring Boot Actuator?

O Spring Boot Actuator inclui vários recursos adicionais para ajudá-lo a monitorar e gerenciar seu aplicativo quando 
você o envia à produção, como por exemplo:

- Endpoint para monitoramento da saúde da aplicação (Health Check).
- Endpoint para expor métricas da aplicação.
- Endpoint para expor as propriedades da sua aplicação.

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

# Configurando segurança

O Spring Boot Actuator fornece muitas APIs interessantes para monitoramento do nosso sistema, contrapartida, essas 
informações podem ser utilizadas para explorar falhas de segurança!

Como assim!?

Vou dar um exemplo, imagina que por algum motivo o recurso de `/actuator/env` está público, ou seja, qualquer um pode 
acesso de qualquer lugar!

Um Hacker, pode por exemplo obter todas as versões das dependências utilizadas no seu projeto e 
explorar falhas, como por exemplo na imagem abaixo:

![alt text](../images/spring-008.png "Spring Boot Actuator")

O Hacker sabe que estou utilizando Spring Boot 2.3.0 e com uma simples pesquisa no google pode encontrar falhas 
relacionadas a esta versão, como por exemplo na imagem abaixo:

![alt text](../images/spring-009.png "Spring Boot Actuator")

Este tópico é bastante importante para todos os projetos da Zup, portanto vamos falar de segurança?

* Gostaria de saber mais sobre segurança? [Aqui tem uma explicação do que entendemos que você deve considerar](../informacao_procedural/seguranca_cloud_native.md)

## Utilizando somente o necessário!

Sabemos que no Spring Boot Actuator existem vários Endpoints e que alguns podem expor informações sensíveis!

Como eu posso remover ou desabilitar meus endpoints?

Existem duas alternativas!

1º Habilitar somente o que é utilizado, para isto é necessário adicionar a propriedade:

`management.endpoints.web.exposure.include=health,metrics` 

2º Remover os não utilizados, para isto é necessário adicionar a propriedade:

`management.endpoints.web.exposure.exclude=env,beans`

# Informação de Suporte

Quer saber mais sobre Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-enabling)