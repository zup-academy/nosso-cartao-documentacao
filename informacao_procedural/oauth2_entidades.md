# Afinal quais são as 4 entidades presentes no OAuth2!!!

Para o perfeito entendimento da especificação OAauth2 é recomendado entender o papel de
cada entidade no fluxo de autenticação.

As 4 entidades são Resource Owner, Resource Server, Client e Authorization Server cada um deles
executa uma atividade bem definida no processo de autenticação.

De uma maneira bastante simplificada as entidades principais interagem da seguinte forma


![oauth 2 basics](../images/oauth2.png "fluxo básico oauth2")


## Informações de suporte

* Talvez você esteja perguntando se existe uma maneira bem simpli
* Você pode estar se perguntando, qual o papel do Resource Server no fluxo?? [Este link pode de te ajudar](https://www.oauth.com/oauth2-servers/the-resource-server/)
  ** Ou ainda você pode estar se perguntando será que o Spring tem alguma coisa relacionado a Resource Sever. [Este link vai ter dar uma visão
  do Resource Server no ecossistema do Spring](https://docs.spring.io/autorepo/docs/spring-security-oauth2-boot/2.0.0.RC2/reference/html/boot-features-security-oauth2-resource-server.html)
* Em Algum momento pode ter surgido uma dúvida sobre o que é AuthorizationServer??   
  