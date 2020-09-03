# Conectando-se no nosso cluster de Kubernetes

Para gerenciar nosso cluster de kubernetes precisamos nos conectá-lo à ele.

Então é hora de fazer isso!

Nosso primeiro passo é garantir que temos a ferramenta de linha de comando do Google
instalada em nossos computadores. 

Você pode estar se perguntando, **"Mas porque eu to ouvindo google se eu cheguei aqui 
buscando informação para me conectar ao cluster de kubernetes?"**. Vamos usar a infraestrutura
do Google para **"servir"** nosso cluster de Kubernetes.

O nome do serviço é **GKE** (Google Kubernetes Engine), e o serviço provê de maneira bastante
efetiva um cluster de Kubernetes com alta-disponibilidade, elasticidade e confiabilidade.

Para nos conectar ao nosso cluster, precisamos, primeiramente autenticar-se usando
a ferramenta de linha de comando. Você pode fazer isso usando o comando:

```shell script
gcloud auth login
```  

Você será redirecionado via browser para o servidor de autenticação do Google.

Leia atentamente as instruções e conclua o processo!

Há qualquer momento você pode acessar o help usando o seguinte comando:

```shell script
gcloud --help
```

Uma vez conectado à conta do Google podemos nos conectar ao nosso cluster, onde o Kubernetes está instalado e operando.

Você pode se conectar ao cluster usando o seguinte comando:

```shell script
gcloud container clusters get-credentials development-bootcamp --zone us-central1-c --project zup-academy
```

Esse comando nos conecta ao nosso cluster. Vamos realizar um pequeno teste para para garantir que nossa
conectividade está funcionando 100%. Utilize o seguinte comando

```
kubectl get namespaces
```

Se o resultado for uma lista de namespaces, aqui não importa o valor deles, sua ferramenta está configurado com sucesso. 

Muito bem, você está conectado!

**Observação** 

Pode ser que no momento da execução da sua tarefa o cluster tenha sido alterado ou está inoperante por conta
de custos, pergunte no nosso canal, caso você tenha algum problema de conexão com o mesmo.

## Informações de suporte

* Talvez você possa estar se perguntando, onde posso achar mais informações sobre o gcloud-sdk. [Este link conta com algumas informações úteis!](https://cloud.google.com/sdk)
  
  * Mas se por algum motivo você não tem a ferramenta instalada, não tem problema, [este link pode te ajudar a instalá-la](https://cloud.google.com/sdk/install)
  
  * Se você se interessou pela ferramenta [este link contém mais uma série de comandos úteis](https://cloud.google.com/sdk/gcloud)

* Se você está se perguntando, onde posso encontrar mais detalhes do serviço GKE, [este link contém algumas informações legais](https://cloud.google.com/kubernetes-engine)   