# Guardando nossos segredos!!! Como criar um secret no kubernetes!!!

Quando desenvolvemos aplicações é comum que elas precisem de algum tipo de configuração para
funcionar, como por exemplo endereço do banco de dados. Usamos ConfigMap do kubernetes para
armazenar as configurações da nossa aplicação separada do código fonte.

Mas, e quando precisamos de valores que não podem ser armazenados de maneira "aberta", sem nenhum
tipo de criptografia??

**ConfigMaps** não são indicados para esse. Precisamos utilizar uma primitiva chamada **Secrets** do Kubernetes.
Essa primitiva permite que consigamos armazenar informações sensíveis como senhas, tokens e chaves SSH.

Vamos ver como podemos declarar um arquivo de configuração de um **Secret**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: proposta
type: Opaque
data:
  username: YWRtaW4=
  password: YWRtaW5AMjYtMjAwLTAtQEA=
```

Note que os valores estão descritos em _Base64_, não é permitido passar os valores "em claro" na criação do elemento

Então agora que declaramos nosso **Secret** vamos utilizar ele em um elemento **Deployment**

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
                  name: proposta
                  key: username
    ## restante omitido
``` 

Note que associamos o **Secret** através da tag **name** apontamos o nome do **Secret** e depois selecionamos o valor que
precisamos utilizar no nosso POD.

Simples!!! Agora você sabe como associar **Secret** + **Pod**!!!

# Informação de Suporte
* Quer saber como criar um ConfigMap no kubernetes esse link pode te ajudar
* Pode ser a primeira vez que você tenha ouvido a palavra base64. [Esse link pode te ajudar a compreender
 um pouco melhor o que é isso](https://developer.mozilla.org/en-US/docs/Glossary/Base64)
* Em algum momento você pode estar se perguntando "Só consigo criar **Secret** via yamls???". [Nesse link você pode descobrir um
    pouco mais como criar secrets usando a ferramenta **kubectl**](https://kubernetes.io/docs/concepts/configuration/secret/#creating-your-own-secrets)
  * Talvez seja a primeira vez que você viu a palavra **kubectl**, não tem problema [esse link vai resolver boa parte da suas dúvidas](https://kubernetes.io/docs/reference/kubectl/overview/)        
* Se você pensou "Então eu posso usar **Secret** e associar minha varíavel de ambiente no meu POD???". Aqui você pode aprender como
    "consumir" o seu **Secret** em um POD.
* Mas se você tem um outro problema "Como posso consumir um **Secret** que esta armazenado um um arquivo???". [Aqui você encontra como
    consumir um **Secret** usando montagem de volume](https://kubernetes.io/docs/concepts/configuration/secret/#using-secrets-as-files-from-a-pod)        