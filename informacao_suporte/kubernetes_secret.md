# Como trabalhar com variáveis de ambiente sensíveis no Kubernetes?

Quando falamos de aplicações cloud-native applications sempre devemos ter em mente o manifesto
do 12 Factor Apps!

Esse manifesto nos ajuda a construir aplicações portáveis entre provedores de nuvem dentre
outras características importantes.

Um dos pilares é o da configuração, que diz que a configuração da aplicação deve ser provida pelo ambiente.

> Quer saber mais sobre configuração no 12 Factor Apps? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/twelve-factor-config.md)

O Kubernetes provê uma série de primitivas, elementos que estão presentes em todas instalações do Kubernetes,
que nos ajudam a lidar com problemas de deployments de aplicações.

Uma delas é o **ConfigMap**, que nos ajuda a manipular informações relacionadas a configuração da aplicação de maneira 
separada, seguindo o pilar do 12 Factor Apps, porém, quando precisamos armazenar informações sensíveis e de forma segura, 
precisamos utilizar uma outra primitiva denominada **Secrets**.

Essa primitiva permite que consigamos armazenar informações sensíveis como senhas, tokens, chaves SSH, etc.

Vamos ver como podemos declarar um arquivo de configuração de um **Secret**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: YWRtaW4=
  password: YWRtaW5AMjYtMjAwLTAtQEA=
```

Você pode salvar um arquivo com qualquer nome com extensão **.yaml** e então ele está apto à ser declarado no Kubernetes!

Demais né!?

Note que temos um nó **data**, qualquer entrada desse nó pode se tornar uma variável de ambiente a ser injetada no [Pod](https://kubernetes.io/docs/concepts/workloads/pods/) 
que for utilizá-la. Dessa maneira se tivermos um sistema que utilize a variável de ambiente **username** ela será 
preenchida com o valor aberto em **Base64**.

Demais né!? Vamos criá-la?

Para criar a Secret no Kubernetes, precisamos executar o seguinte comando:

```shell script
$ kubectl apply -f <NOME DO SEU ARQUIVO>.yaml
```

> Está em dúvida de como se conectar no cluster Kubernetes? Não se preocupe! [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/conectando_gcloud_sdk.md)

Eba! Você criou sua primeira Secret no Kubernetes!

>  Talvez esteja se perguntando existe alguma lista de comandos mais utilizados? [Aqui você encontra essa lista!](kubernetes_kubectl.md)

## Associando Secret ao [PODs](https://kubernetes.io/docs/concepts/workloads/pods/)

Uma vez que declaramos nossas variáveis de ambiente no **Secret**, podemos utilizá-la em nossos PODs, onde efetivamente
rodam nossas aplicações. Para fazer isso devemos adicionar a seguinte configuração no arquivo de configuração de deployments,
conforme exemplo abaixo:

```yaml
## restante omitido
spec:
  containers:
    - image: zupacademy/proposta
      imagePullPolicy: Always
      env:
        - name: USERNAME
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: username
## restante omitido
``` 

A associação acontece pela configuração do nó **valueFrom** perceba que referenciamos o **Secret** pelo atributo
**secretKeyRef**.

Demais né!?

# Informação de Suporte

* Talvez esteja se perguntando o que é Base64, não se preocupe,  [aqui tem uma explicação do que entendemos que você deve considerar](https://pt.wikipedia.org/wiki/Base64)

* Gostaria de saber mais sobre Secret? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://kubernetes.io/docs/concepts/configuration/secret/)

* Gostaria de saber mais detalhes sobre Secret e Pod? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://kubernetes.io/docs/concepts/configuration/secret/#using-secrets-as-environment-variables)

* Talvez esteja se perguntando, como eu criou um deployment no Kubernetes? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_suporte/kubernetes_deployment.md) 