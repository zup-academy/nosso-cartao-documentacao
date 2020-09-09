# Como trabalhar com variáveis de ambiente no Kubernetes?

Quando falamos de aplicações cloud-native applications sempre devemos ter em mente o manifesto
do 12 Factor Apps!

Esse manifesto nos ajuda a construir aplicações portáveis entre provedores de nuvem dentre
outras características importantes.

Um dos pilares é o da configuração, que diz que a configuração da aplicação deve ser provida pelo ambiente.

> Quer saber mais sobre configuração no 12 Factor Apps? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/twelve-factor-config.md)

O Kubernetes provê uma série de primitivas, elementos que estão presentes em todas instalações do Kubernetes,
que nos ajudam a lidar com problemas de deployments de aplicações.

Uma delas é o **ConfigMap**, que nos ajuda a manipular informações relacionadas a configuração
da aplicação de maneira separada, seguindo o pilar do 12 Factor Apps.

Então vamos entender como podemos declarar um ConfigMap 

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  LOG_LEVEL: "INFO"
  SERVER_PORT: "8888"
```

Você pode salvar um arquivo com qualquer nome com extensão **.yaml** e então ele está apto à ser declarado no Kubernetes!

Demais né!?

Note que temos um nó **data**, qualquer entrada desse nó pode se tornar uma variável de ambiente a ser injetada no [Pod](https://kubernetes.io/docs/concepts/workloads/pods/) 
que for utilizá-la. Dessa maneira se tivermos um sistema que utilize a variável de ambiente **SERVER_PORT** ela será 
preenchida com o valor **8888**.

Demais né!? Vamos criá-lo?

Para criar o ConfigMap no Kubernetes, precisamos executar o seguinte comando:

```shell script
$ kubectl apply -f <NOME DO SEU ARQUIVO>.yaml -n <NAMESPACE>
```

> Está em dúvida de como se conectar no cluster Kubernetes? Não se preocupe! [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/conectando_gcloud_sdk.md)

Eba! Você criou seu primeiro ConfigMap no Kubernetes!

>  Talvez esteja se perguntando existe alguma lista de comandos mais utilizados? [Aqui você encontra essa lista!](kubernetes_kubectl.md)

## Associando ConfigMap ao [PODs](https://kubernetes.io/docs/concepts/workloads/pods/)

Uma vez que declaramos nossas variáveis de ambiente no **ConfigMap**, podemos utilizá-la em nossos PODs, onde efetivamente
rodam nossas aplicações. Para fazer isso devemos adicionar a seguinte configuração no arquivo de configuração de deployments,
conforme exemplo abaixo:

```yaml
## restante omitido
spec:
  containers:
    - image: zupacademy/contas
      imagePullPolicy: Always
      envFrom:
        - configMapRef:
            name: my-config
## restante omitido
``` 

A associação acontece pela configuração do nó **envFrom** perceba que referenciamos o **ConfigMap** pelo atributo
**configMapRef**, o elemento **ConfigMap** deve ter sido configurado previamente.

**Observação**: **ConfigMap** deve ser utilizado para armazenar configurações não confidenciais, ou seja, 
não há algum mecanismo de criptografia associado. Este modelo **NÃO** deve ser utilizado para armazenar
senhas ou informações sigilosas.

Gostaria de para armazenar senhas ou informações sigilosas no Kubernetes? [Aqui você encontra como fazer isso!](../informacao_suporte/kubernetes_secret.md)

# Informação de Suporte

* Gostaria de saber mais sobre ConfigMap? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://kubernetes.io/docs/concepts/configuration/configmap/)

* Gostaria de saber mais detalhes sobre ConfigMap e Pod? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://kubernetes.io/docs/concepts/configuration/configmap/#configmaps-and-pods)

* Talvez esteja se perguntando, como eu criou um deployment no Kubernetes? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_suporte/kubernetes_deployment.md)