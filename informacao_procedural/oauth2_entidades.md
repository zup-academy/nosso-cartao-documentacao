# Afinal, quais são as 4 entidades presentes no OAuth2!!!

Para o perfeito entendimento da especificação OAauth2 é recomendado entender o papel de
cada entidade no fluxo de autenticação.

As 4 entidades são Resource Owner, Resource Server, Client e Authorization Server cada um deles
executa uma atividade bem definida no processo de autenticação.

De uma maneira bastante simplificada as entidades principais interagem da seguinte forma, uma parte bastante 
relevante é que o oauth permite alguns modelos de autenticação com mais ou menos interações entre o cliente
e o authorization server, mas não se preocupe vamos cobrir todos os detalhes.


![oauth 2 basics](../images/oauth2.png "fluxo básico oauth2")


## Informações de suporte
* Você pode estar se perguntando, qual o papel do **Resource Server** no fluxo?? [Este link pode de te ajudar](https://www.oauth.com/oauth2-servers/the-resource-server/)
  * Ou ainda você pode estar se perguntando será que o Spring tem alguma coisa relacionado a Resource Sever. [Este link vai ter dar uma visão
  do Resource Server no ecossistema do Spring](https://docs.spring.io/autorepo/docs/spring-security-oauth2-boot/2.0.0.RC2/reference/html/boot-features-security-oauth2-resource-server.html)
* Em Algum momento pode ter surgido uma dúvida sobre o que é **Authorization Server**??
  * Você pode estar se perguntando, "Será que o Spring pensou em alguma solução para nos ajuda??". Sim, o Spring tem um projeto que nos ajuda
  a implementar um Authorization Server. [Aqui você pode encontrá-lo](https://github.com/spring-projects-experimental/spring-authorization-server). Mas, lembre-se é uma tarefa bastante 
  difícil e precisa de bastante conhecimento de segurança.   
  * Ou você pode estar se perguntando, Como eu posso conseguir encontrar os serviços que o Authorization Server
  expõe para minha utilização, um Authorization Server deve expor um serviço para podermos encontrar o que
  podemos fazer nele. [Aqui você pode encontrar uma parte da especificação](https://tools.ietf.org/html/rfc8414)
   * Uma parte legal é que essa parte da especificação já menciona integração com OpenID Connect. [Aqui você pode encontrar
   esse conteúdo](https://tools.ietf.org/html/rfc8414#section-1)
  * Você pode estar se perguntando, já que vamos utilizar nosso IAM para gerar nossos tokens, o que automaticamente faz com que ele
  atue como **Authorization Server**, onde posso encontrar os metadados do servidor? 
    * O Keycloak cria uma separação de usuários,credencias, grupos e permissões por Realm, então cada Realm tem seus metadados.
    * Talvez você possa estar se perguntando. Mas pera ae o que é um Realm?? [Nesta seção da documentação você pode encontrar a descrição](https://www.keycloak.org/docs/latest/server_admin/#core-concepts-and-terms)
      * Ou ainda você pode estar se perguntando como criar um Realm, [neste link você pode encontrar um passo-a-passo de como fazer isso](realm_keycloak.md)     
    * Se em algum momento você quiser consultar os metadados do nosso Authentication Server, [nesse link você pode encontrar](http://localhost:18080/auth/realms/nosso-cartao/.well-known/openid-configuration)
      * Se você quiser entender um pouco do well-know, você pode consultar na [RFC](https://tools.ietf.org/html/rfc8615)
* Se por algum motivo você ficou com alguma dúvida sobre o papel do resource owner, não tem problema esse [link vai ter algumas informações](https://tools.ietf.org/html/draft-ietf-oauth-v2-16#section-1.1)
  * Talvez não esteja 100% o papel do Resource Owner, [aqui tem uma material feito pela equipe do academy para te ajudar com essa dúvida](oauth2_resource_owner.md)
* Em algum momento você pode estar se perguntando, qual é a função do client no OAuth           