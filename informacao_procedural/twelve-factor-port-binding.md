# Vínculo de Portas. VII do 12 Factor Apps

Nossas aplicações devem expor seus serviços web via vínculos de portas.

Servidores de aplicação ou WebServer eram e são bastante comuns em ambientes
não cloud.

Uma característica bastante importante é que esses servidores (onde instalamos
nossas aplicações) eram responsáveis por gerenciar as portas das nossas aplicações.
Eles tinham o poder de escolher uma porta e associá-la à nossa aplicação.

Em ambiente cloud, nossas aplicações devem ser auto-contidas, ou seja, nossas aplicações
são responsáveis por "subir" o serviço e fazer o vínculo das portas. Nunca
nossas aplicações devem ser instaladas em um servidor de aplicação externo.

Um exemplo dessa prática é o Spring Boot que automaticamente sobe um servidor web, Tomcat por exemplo, 
e consegue mantê-lo em pé disponibilizando uma porta de acesso à nossas APIs.

## Informações de suporte

* Talvez você possa se perguntar, o que é Tomcat. [Aqui você pode encontrar uma definição](http://tomcat.apache.org/)



