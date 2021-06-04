# Tenho meu Dockerfile, e agora qual comando do docker devo usar para criar minha imagem?

Temos nosso Dockerfile, vamos entender agora como realizar a construção da imagem.

O primeiro passo é chegar no diretório onde está nosso Dockerfile, dentro desse diretório podemos executar o comando:

```shell script
docker image build -t zupacademy/proposta:latest .
```

Massa, parece que esse comando tem alguns parâmetros, vamos entendê-los?

O **docker image** no início do comando indica que vamos utilizar a API de imagens. Logo depois encontramos a flag **-t** 
nesse caso colocamos um nome e a tag o nome é composto pelo **usuário/nome** da imagem. No nosso caso estamos usando o
docker hub um repositório público de imagens, por isso seguimos esse padrão, dependendo do seu vendor de Registry esse 
padrão pode mudar ligeiramente.

O ponto final no final do comando indica o contexto da build, por esse motivo utilizamos **.** na raiz do diretório.

Eba! Nossa imagem foi gerada! Vamos testá-la?

Para isso, escrevemos um [material específico para você!](../informacao_procedural/comando-run-docker.md)

## Informações de suporte

* Talvez você esteja se perguntando, como instalar o Docker? [Esse link pode te ajudar com isso!](https://docs.docker.com/get-docker/)

* Talvez você esteja se perguntando, tem algum jeito de customizar ainda mais esse comando? A resposta é sim! [Esse link pode te ajudar com isso!](https://docs.docker.com/engine/reference/commandline/image_build/) 

* Está em dúvida sobre o que é um Registry? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://docs.docker.com/registry/)
  
* No material anterior você viu o que é um Registry, você sabia que pode executar localmente? [Esse link pode te ajudar com isso!](https://docs.docker.com/registry/deploying/)
