# Tenho meu Dockerfile, e agora qual comando do docker devo usar para criar minha imagem??

Legal, temos nosso Dockerfile, vamos entender agora como realizar a construção
da imagem.

O primeiro passo é chegar no diretório aonde esta nosso Dockerfile, dentro desse 
diretório podemos executar o comando 

```shell script
docker image build -t zupacademy/proposta:latest .
```

Massa, parece que esse comando tem alguns parâmetros vamos entendê-los

**docker image** no início do comando indica que vamos utilizar a API de imagens. Logo depois
encontramos a flag **-t** nesse caso colocamos um nome e a tag o nome é composto pelo **usuario/nome** da imagem. No nosso caso
estamos usando o dockerhub um repositório público de images, por isso
seguimos esse padrão, dependendo do seu vendor de Registry esse padrão pode mudar ligeiramente.
O ponto final no final do comando indica o contexto da build, por esse motivo utilizamos **.**, estamos na raíz


# Informações de suporte

* Talvez você possa querer instalar o docker na sua máquina. [Esse link pode te ajudar com isso!!!](https://docs.docker.com/get-docker/)
* Ou ainda você queira saber todos as opções do comando docker image. Nesse caso recomendamos você
se aprofundar na [documentação do comando](https://docs.docker.com/engine/reference/commandline/image/)
* Talvez você esteja se perguntando, tem algum jeito de customizar ainda mais esse comando. A resposta é sim,
[aqui você encontra](https://docs.docker.com/engine/reference/commandline/image_build/) 
* Em algum momento você deve estar se perguntando "O que é um Registry???". [Na documentação do docker você pode encontrar isso](https://docs.docker.com/registry/)
  * Mas, se você gostaria de se aprofundar e rodar um docker registry local. [Tem como fazer isso!!!](https://docs.docker.com/registry/deploying/)
* Ou ainda se você gostaria de saber o que é dockerhub, sugerimos dar uma olhada [no site, ta bem tranquilo de entender!!!](https://hub.docker.com/)

