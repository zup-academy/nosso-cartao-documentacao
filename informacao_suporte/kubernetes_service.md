# Pronto para expor nossa aplicação, entendendo um pouco mais de kubernetes services!

Depois de instalarmos nossa aplicação em um cluster Kubernetes precisamos encontrar um jeito
de expor essa aplicação em um endereço de rede válido dentro do cluster.

Cada POD do Kubernetes tem um endereço de IP único dentro do cluster, levando em consideração
as configurações da rede interna do cluster.

Agora imagine a seguinte situação, em um cluster kubernetes POD nascem e "morrem" com
bastante frequência isso faz parte da maneira como o kubernetes gerência nosso workload.

Agora imagine que você precise identificar um POD na rede pelo IP, levando em consideração que o POD pode
ser destruído a qualquer momento, nosso endereço de IP parece não ser confiável já que a troca pode
ocorrer à qualquer momento.

Precisamos de uma maneira que nos ajude a _"mapear"_ esses PODs em um único endereço de rede. Além de criar esse
mapeamento precisamos de comportamentos como Load Balance, por exemplo, imagine que temos
8 instâncias de um mesmo serviço não queremos que todo request passe pela mesma instância, gostaríamos de poder
se beneficiar de uma estratégia de balanceamento de carga a fim de não causar carga excessiva em um único POD.

Para esses casos de uso o Kubernetes possui uma primitiva chamada **Services**, essa primitiva permite que criemos uma
abstração lógica para um conjunto de PODs. Esses PODs são selecionados através de Labels Selectors e então o Kubernetes
cria uma espécie de nome na rede para agrupá-los, dessa maneira não precisamos utilizar IPs para controlar nossos endereços.

Isso nos dá uma característica de **Service Discovery** também já que o Kubernetes consegue manter um _catálogo_ de PODs para 
receber as requisições!

Então já que sabemos o que é um **Service**, vamos ver um arquivo de configuração!

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: analise
  name: analise
spec:
  ports:
    - name: http
      port: 8888
      protocol: TCP
      targetPort: 8888
  selector:
    app: analise
```

Temos algumas informações importantes no arquivo. Note que temos um elemento **ports**, ele elemento indica 
as portas de rede que o serviço vai estar _"listening"_ também podemos perceber que estamos declarando a qual porta
do POD ele vai **"redirecionar"** o tráfego.

Outra parte muito importante é o **selector** perceba que "selecionamos" todos os PODs que
possuem a label **"app: analise"** . Isso indica que criamos nosso agrupamento lógico de PODs que
atendem pelo nome do serviço **análise.**
 
Pronto! Você está pronto para criar seu **Service**!

Demais né!? Vamos criá-lo?

Para criar o Service no Kubernetes, precisamos executar o seguinte comando:

```shell script
$ kubectl apply -f <NOME DO SEU ARQUIVO>.yaml -n <NAMESPACE>
```

> Está em dúvida de como se conectar no cluster Kubernetes? Não se preocupe! [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/conectando_gcloud_sdk.md)

Eba! Você criou seu primeiro Service no Kubernetes!

>  Talvez esteja se perguntando existe alguma lista de comandos mais utilizados? [Aqui você encontra essa lista!](kubernetes_kubectl.md)

# Informação de Suporte

* Talvez você nunca tenho escutado a palavra POD, não tem problema. [Esse link explica detalhadamente isso](https://kubernetes.io/docs/concepts/workloads/pods/) 

* Talvez você pode estar se perguntando "Service Discovery???". [Esse link tem algumas noções básicas da técnica](https://www.nginx.com/blog/service-discovery-in-a-microservices-architecture/)
  
  * Se você quer entender um pouco mais da motivação da técnica de Service Discovery. [Aqui você pode encontrá-la](https://www.nginx.com/blog/service-discovery-in-a-microservices-architecture/#Why-Use-Service-Discovery)

* Talvez você possa estar se perguntando "Mas porque eu iria precisar de um outro elemento do kubernetes pra isso?". [Esse link explica algumas
motivações por trás do conceito](https://kubernetes.io/docs/concepts/services-networking/service/#motivation)

* Service Discovery??? Como o kubernetes **Service** consegue resolver isso?? [Aqui você encontra uma breve descrição do funcionamento](https://kubernetes.io/docs/concepts/services-networking/service/#cloud-native-service-discovery) 

* Se vocẽ tem alguma dúvida de como DNS do cluster se integra com o kubernetes **Service**. [Esse link tem algumas informações importantes
para você descobrir como será criado o DNS do ser **Service**](https://kubernetes.io/docs/concepts/services-networking/service/#cloud-native-service-discovery) 

* Em algum momento você pode estar pensando "Existem tipos de **Services** no kubernetes?? E se eu precisar de um **Service** que tenha comportamentos de Load Balancer??"
  [Esse link tem a definição de todos os tipos de **Service** que o kubernetes suporta!!!](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types). 
  E para nossa alegria tem tipo **Load Balancer**!!!

* Você pode estar se perguntando "O que são Labels e Selectors". Labels são muito importantes para o kubernetes é de certa forma
  uma maneira de você "marcar" um objeto. [Aqui você encontra uma explicação bem legal sobre isso](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

  * Ou ainda você pode estar perguntando "Porque eu preciso de Labels". [Aqui tem uma boa motivação pra isso](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#motivation)  

* Em algum momento você pode ter se perguntando "Como eu combino a utilização de Labels + Selectors" . [Esse link pode sanar essa dúvida](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#label-selectors)
