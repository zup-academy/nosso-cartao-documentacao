# Configurando nossa aplicação como Resource server

Definimos que nosso sistema de **proposta** vai se comportar como **Resource Server** definido
no padrão OAuth. 

Lembre-se que você já deve ter um Realm no Keycloak previamente criado! Caso você tenha alguma
dúvida de como fazer isso. Temos um material que pode te ajudar na seção _Informação de Suporte_.

Então vamos configurar nossa aplicação para atuar como esta entidade!

No primeiro passo vamos adicionar as dependências necessárias do Spring Security!

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-oauth2-jose</artifactId>
</dependency>
```

A primeira dependência nos ajuda a configurar nossa aplicação como Resource Server, já na segunda dependência configuramos
o Spring Framework para interações com Tokens JWT, essa lib nos ajudar a _"abrir"_ o token
e manipulá-lo com classes java, o que nos ajuda muito!

No próximo passo precisamos indicar nosso emissor de token e o endereço onde podemos encontrar
as chaves e algoritmos  para validar nossos tokens JWT. Então vamos fazer isso!

```properties
## spring security resource server configuration
spring.security.oauth2.resourceserver.jwt.issuer-uri=${KEYCLOAK_ISSUER_URI:http://localhost:18080/auth/realms/nosso-cartao}
spring.security.oauth2.resourceserver.jwt.jwk-set-uri=${KEYCLOAK_JWKS_URI:http://localhost:18080/auth/realms/nosso-cartao/protocol/openid-connect/certs}
```

A primeira configuração _spring.security.oauth2.resourceserver.jwt.issuer-uri_ nos ajuda a informar onde o Spring Security
pode encontrar nosso authorization server. Essa informação é muito importante!

Já nossa segunda configuração _spring.security.oauth2.resourceserver.jwt.jwk-set-uri_, indicamos onde o Spring Security 
pode encontrar as chaves para conseguir validar a assinatura do token.

Bem simples como com esses passos já configuramos nossa aplicação para ser um Resource Server.

O nosso próximo passo é fazer com que o Spring Boot autorize nossas requisições de acordo com o token recebido e com 
base em seus dados permitir o processamento da requisição ou bloquear a mesma.

Se você acha que está pronto. Que tal partir para resolver esse próximo passo. [Aqui você encontra como
realizar essa configuração no Spring Security](oauth-spring-security-auth.md)

## Informação de Suporte

* Talvez sua primeira dúvida pode ter sido mas afinal de contas _"o que é um realm?"_ Não se preocupe
com isso, [este link vai te ajudar com isso](https://www.keycloak.org/docs/latest/server_admin/#core-concepts-and-terms)

  * Ainda pode estar se perguntando "Como eu posso criar um realm no keycloak?". [Este link tem um passo-a-passo
  de como fazer isso!!](keycloak-realm.md)
  
* Caso você nunca tenha ouvido a palavra JWT, não tem problema [aqui tem uma boa introdução sobre o tema!](https://jwt.io/introduction/)  

  * Se você quer visitar a RFC e entrar em profundidade sobre o JWT, [este link vai te ajudar a navegar na RFC](https://tools.ietf.org/html/rfc7519) 
   
* Se em algum momento você se perguntou "Onde está a documentação oficial do Spring sobre Resource Server?". [Este link vai te ajudar a se aprofundar](https://docs.spring.io/spring-security/site/docs/current/reference/html5/#oauth2resourceserver)  
