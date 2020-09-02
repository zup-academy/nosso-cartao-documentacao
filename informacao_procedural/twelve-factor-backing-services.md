# Backing Services. IV do 12 Factor Apps

Nossas aplicações não vivem sozinhas na grande maioria dos casos, elas precisam interagir com alguns serviços externos. 
Por exemplo, precisamos armazenar os estados dos nossos objetos em um banco de dados relacional, esse banco de dados está
instalado "fora" da nossa aplicação.

_Lembre-se do princípio **VI Processos**, execute sua aplicação de maneira que ela tenha o mínimo de estado possível._

Nesse caso nosso banco de dados é considerado como um "Backing Service", ou seja um serviço externo, que nossa aplicação consome
via rede. A configuração desses serviços normalmente se dão via config, apontando para um endereço de rede onde o elemento
está instalado.

Cada Backing Service pode ser chamado de um recurso, por exemplo um Recurso de Mensageria RabbitMQ

## Informações de suporte

* Se você ainda está com alguma dúvida sobre o que é Backing Service, [esse link pode te ajudar](https://12factor.net/backing-services)

* Se você está se perguntando mas como eu posso configurar meus **Backing Services**, [este link aponta para o fator III - Config que pode te dar
algumas pistas](https://12factor.net/config)


