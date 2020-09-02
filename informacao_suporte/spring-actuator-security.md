# Como configurar segurança no Spring Boot Actuator?

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

`management.endpoints.web.exposure.include=health,metrics,prometheus` 

2º Remover os não utilizados, para isto é necessário adicionar a propriedade:

`management.endpoints.web.exposure.exclude=env,beans`

## Utilizando CORS!

O CORS (Cross-origin Resource Sharing) é um mecanismo utilizado pelos navegadores para compartilhar recursos entre 
diferentes origens. O CORS é uma especificação do W3C e faz uso de headers do HTTP para informar aos navegadores se 
determinado recurso pode ser ou não acessado.

Permitindo receber somente de uma origem, aumenta demais a segurança das APIs do Spring Boot Actuator!

Para isto, basta adicionar as seguintes propriedades no arquivo `application.properties`:

```properties
management.endpoints.web.cors.allowed-origins=https://example.com
management.endpoints.web.cors.allowed-methods=GET
```

## Dicas de Luram Archanjo

Não deixe pública sua API, alinhe sempre com sua equipe as melhores práticas, como por exemplo:

- Adicionar autenticação
- Adicionar autorização

## Dicas de Claudio Eduardo Oliveira

Não negligencie as informações que você está expondo sobre a sua infraestrutura.

# Informação de Suporte

Quer saber mais sobre Spring Boot Actuator? Acesse o [link!](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-enabling)

Quer saber mais sobre o The Twelve-Factor App? Acesse o [link!](https://12factor.net/pt_br/)