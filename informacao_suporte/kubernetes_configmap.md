# Como trabalhar com variáveis de ambiente do Kubernetes?

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
  name: contas-config
data:
  LOG_LEVEL: "INFO"
  SERVER_PORT: "8888"
```

Você pode salvar um arquivo com qualquer nome com extensão **.yaml** e então ele está apto à ser declarado no Kubernetes!

Demais né!?

Note que temos um nó **data**, qualquer entrada desse nó pode se tornar uma variável de ambiente a ser injetada no [Pod](https://kubernetes.io/docs/concepts/workloads/pods/) 
que for utilizá-la. Dessa maneira se tivermos um sistema que utilize a variável de ambiente **SERVER_PORT** ela será 
preenchida com o valor **8888**.

Demais né!?

## Associando ConfigMap ao [PODs](https://kubernetes.io/docs/concepts/workloads/pods/)

Uma vez que declaramos nossas varíaveis de ambiente no **ConfigMap**, podemos utilizá-la em nossos PODs, onde efetivamente
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
            name: contas-config
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

* Ou ainda você pode ter ficado em dúvida em como criar um deployment, [neste link tem o passo a passo de como fazer isso](kubernetes_deployment.md)

* Talvez você queira entrar em mais detalhes de como podemos associar ConfigMap e PODs, [este link pode te ajudar com isso](https://kubernetes.io/docs/concepts/configuration/configmap/#configmaps-and-pods)

* Talvez você possa estar se perguntando "Então quando eu atualizo meu ConfigMap, o POD automaticamente faz o reload da varíavel??". 
  Na verdade esse não é um comportamento padrão, mas [esse link pode te ajudar a chegar nesse comportamento](https://kubernetes.io/docs/concepts/configuration/configmap/#mounted-configmaps-are-updated-automatically)