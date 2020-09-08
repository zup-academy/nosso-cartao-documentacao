# Comandos mais utilizados no Kubernetes!

## Buscar primitivas do Kubernetes

##### Buscar todos namespaces
```shell script
kubectl get namespaces
```

##### Buscar todos PODs de todos os namespaces
```shell script
kubectl get pods --all-namespaces
```

##### Buscar todos PODs de um determinado namespace
```shell script
kubectl get pods -n <namespace>
```

##### Buscar todos Services de um determinado namespace
```shell script
kubectl get services -n <namespace>
```

##### Buscar todos Deployments de um determinado namespace
```shell script
kubectl get deployments -n <namespace>
```

##### Buscar todos ConfigMaps de um determinado namespace
```shell script
kubectl get configmaps -n <namespace>
```

## Buscar primitivas (por name) do kubernetes

##### Buscar POD pelo name de um determinado namespace
 
```shell script
kubectl get pods <pod_name> -n <namespace>
```

##### Buscar Service pelo name de um determinado namespace
 
```shell script
kubectl get service <service_name> -n <namespace>
```

##### Buscar Deployment pelo name de um determinado namespace
 
```shell script
kubectl get deployments <deployment_name> -n <namespace>
```

## Buscando objetos do kubernetes com formatação

##### Buscar Deployment pelo name de um determinado namespace e verificar o conteúdo em formato yaml
 
```shell script
kubectl get deployments <deployment_name> -n <namespace> -o yaml
```

##### Buscar Deployment pelo name de um determinado namespace e verificar o conteúdo em formato json
 
```shell script
kubectl get deployments <deployment_name> -n <namespace> -o json
```

# Informação de Suporte

Gostaria de saber mais sobre os comandos do kubectl? Acesse o [link!](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)