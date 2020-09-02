# Porque Health Check?

Uma característica bastante importante que sua aplicação deve implementar é o **Health Check**.
 
Nossas aplicações normalmente rodam em um ambiente gerenciado, ou seja, uma plataforma que é capaz de detectar se alguma 
coisa não está funcionando conforme o esperado, um _crash_ de aplicação ou carga demasiada.

Depois de notar essas falhas essas plataformas são capazes de tomar algumas ações para tentar remediar a aplicação, 
reiniciar ou mesmo desligar a aplicação e lançá-la novamente em outro servidor.

Para que isso funcione precisamos expor alguma operação em nossa aplicação para que a plataforma possa chamar e verificar 
se tudo está funcionando perfeitamente.

Temos algumas alternativas, quando nossa aplicação expõe uma _API REST_ podemos usar um
endpoint _HTTP GET_ para esse fim, esse endpoint deve verificar se o que a aplicação
precisa para funcionar está 100% operacional. Isso pode incluir banco de dados e serviços de
mensageria por exemplo.

Entretanto, se nossa aplicação é uma aplicação de processamento em lote ou batch, podemos expor uma
funcionalidade via linha de comando, seguindo os mesmo princípios, ou seja, validando
conexões externas da nossas aplicações.

# Dicas de Cláudio

- Incorpore esse padrão nos seus serviços, de maneira que todo serviço seja produzido já implementando esse padrão.

# Informações de Suporte

- O **Spring Boot** oferece uma maneira eficiente de lidar com Health Check. [Aqui](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html) você pode descobrir como.

- Se você quer descobrir como o **Kubernetes** utiliza seu Health Check para garantir que sua aplicação
esteja viva. Esse [link](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) vai resolver o seu problema.

- Este padrão é bastante comum na arquitetura de Microsserviços, se você deseja ver uma descrição
detalhada, esse [link](https://microservices.io/patterns/observability/health-check-api.html) é uma boa opção.


