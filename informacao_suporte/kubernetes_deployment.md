# Então vamos por nossa aplicação para RODAR, como realizar o deployment da nossa aplicação!

Quando vamos rodar nossa aplicação precisamos garantir alguns controles, como por
exemplo número de réplicas ativas, estratégias de rollback quando há uma falha na nova
versão, suportar regras de auto-scaling quando há pico de carga dentre outros.

O Kubernetes provê uma forma mais centralizada de nos ajudar com isso através do elemento
Deployment, que na prática significa controlar um grupo de PODs com características similares.

Por exemplo quando temos uma aplicação de **fatura**, todos os PODs dessa mesma aplicação possuem
as mesmas características, como imagem do container, limites de recursos. Caso seja
necessário realizar alguma operação nesses PODs idealmente gostaríamos que fossem aplicadas
para todos que possuem essa mesma característica.

Neste ponto o elemento **Deployment** nos ajuda, controlar um grupo de PODs que possuem as mesmas características.

Quando pensamos em manter nossas aplicações rodando certamente alguns atributos já nos vem à cabeça:

* Número de réplicas
* Nome da imagem que nossa aplicação é empacotada 
* Talvez histórico de revisões 

Perceba que esses detalhes são relacionados a nossa aplicação, que de certa forma caracterizam ela.

Também precisamos informar no nosso **Deployment** algumas informações relacionadas a infraestrutura necessária para rodar
nossa aplicação bem como detalhes para que nossa infraestrutura seja informada que nossa aplicação está funcionando 
corretamente.

* **Liveness Probe** e **Readiness Probe** são informações que devemos informar para que o Kubernetes entenda a situação atual da nossa aplicação 
* **Recursos** necessários para rodar nossa aplicação como por exemplo 512 MB de RAM e 1 CPU. Esta informação o kubernetes irá
utilizar para acondicionar melhor nosso POD, considerando limites computacionais de cada máquina do Cluster.

Esses itens são **MUITO** importantes para o correto funcionamento da nossa aplicação no cluster.

Então agora que sabemos a necessidade de se criar um deployment vamos para um exemplo prático!

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    version: v1
    app: contas
    team: cartao-branco
  name: contas
spec:
  replicas: 1
  selector:
    matchLabels:
      app: contas
  template:
    metadata:
      labels:
        app: contas
        version: v1
    spec:
      containers:
        - image: zupacademy/contas
          imagePullPolicy: Always
          envFrom:
            - configMapRef:
                name: contas-config
          resources:
            requests:
              memory: "256Mi"
              cpu: "700m"
            limits:
              memory: "512Mi"
              cpu: "900m"
          livenessProbe:
            httpGet:
              path: /actuator/health
              port: 8888
              scheme: HTTP
            initialDelaySeconds: 60
          name: contas
          ports:
            - containerPort: 8888
              name: http
              protocol: TCP
          readinessProbe:
            httpGet:
              path: /actuator/health
              port: 8888
              scheme: HTTP
            initialDelaySeconds: 60
```

Talvez o detalhe mais importante seja o nó **containers**, note que essa configuração é uma lista. Isso mesmo um _POD_ pode conter 
mais de um container, não há restrições à isso. Declaramos uma imagem do nosso legado **zupacademy/contas**, que na verdade é um 
sistema que controla cartões.

Note que declaramos limite computacionais usando a tag **resources**, na tag **requests** informamos o patamar mínimo que a aplicação
já precisa de início. Na tag **limits** já definimos o patamar mais alto, caso a aplicação chegue nesse limite o kubernetes vai tomar de ação
de derrubar o POD e levantá-lo imediatamente.  

Outra configuração **MUITO** importante é relacionado aos Probes, perceba que nossa aplicação precisa expor esses endpoints, no nosso caso
o Spring Boot Actuator já nos ajuda com isso!!! Com essas informações o kubernetes é capaz de decidir se a aplicação está saudável ou que seja 
necessário realizar alguma ação.

E aí pronto para fazer seu primeiro arquivo de configuração de deployment!!!!

Demais né!? Vamos criá-lo?

Para criar o Deployment no Kubernetes, precisamos executar o seguinte comando:

```shell script
$ kubectl apply -f <NOME DO SEU ARQUIVO>.yaml -n <NAMESPACE>
```

> Está em dúvida de como se conectar no cluster Kubernetes? Não se preocupe! [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/conectando_gcloud_sdk.md)

Eba! Você criou seu primeiro Deployment no Kubernetes!

>  Talvez esteja se perguntando existe alguma lista de comandos mais utilizados? [Aqui você encontra essa lista!](kubernetes_kubectl.md)

# Informação de Suporte

* Você pode estar se perguntando "Ainda não tenho certeza o que é um POD", [este link pode te ajudar a compreender um pouco mais sobre isso](https://kubernetes.io/docs/concepts/workloads/pods/)

* Talvez você possa estar em dúvida sobre algum item relacionado ao Liveness Probe e Readiness Probe. [Esse link tem algumas dicas bem legais sobre isso](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

* Ou ainda você queira se aprofundar em como o Liveness Probe e Readiness Probe influência no ciclo de vida de um POD. [Esse link indica algumas situações que você deve considerá-los](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#when-should-you-use-a-liveness-probe)

* Se por algum motivo você ainda está com dúvidas sobre a configuração de limites de recursos computacionais, [esse link pode te ajudar a entender melhor](https://cloud.google.com/blog/products/gcp/kubernetes-best-practices-resource-requests-and-limits)

* Se você tem alguma dúvida sobre o Spring Boot Actuator, [esse link pode ajudá-lo](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html)