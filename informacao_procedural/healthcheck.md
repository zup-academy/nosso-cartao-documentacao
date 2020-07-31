# Porque healthcheck ???

Uma característica bastante importante que sua aplicação deve implementar é o **Healthcheck**.
 
Nossas aplicações normalmente rodam em um ambiente gerenciado, ou seja uma plataforma que é capaz de detectar se alguma coisa não está
funcionando conforme o esperado, um _crash_ de aplicação ou carga demasiada.

Depois de notar essas falhas essas plataformas são capazes de tomar algumas ações para tentar remediar a aplicação, reiniciar
ou mesmo derrubar a aplicação e lançá-la novamente em outro servidor.

Para que isso funcione precisamos expor alguma operação em nossa aplicação para que
a plataforma possa chamar e verificar se tudo esta funcionando perfeitamente.

Temos algumas alternativas, quando nossa aplicação expõe uma _API REST_ podemos usar um
endpoint _HTTP GET_ para esse fim, esse endpoint deve verificar se o que a aplicação
precisa para funcionar está 100% operacional. Isso pode incluir banco de dados e serviços de
mensageria por exemplo.

Mas se nossa aplicação é uma aplicação de processamento em lote, ou batch podemos expor uma
funcionalidade via linha de comando, seguindo os mesmo princípios, ou seja validando
conexões externas da nossas aplicações.

## Informações de Suporte

O **Spring Boot** oferece uma maneira eficiente de lidar com healthchecks. [Aqui](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html) você pode descobrir como.

Se você quer descobrir como o **kubernetes** utiliza seu healthcheck para garantir que sua aplicação
esteja viva. Esse [link](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) vai resolver o seu problema.

Este padrão é bastante comum na arquitetura de microsserviços, se você deseja ver uma descrição
detalhada, esse [link](https://microservices.io/patterns/observability/health-check-api.html) é uma boa opção.