# Primeiros passos para criação de uma imagem Docker

O primeiro passo para criar uma imagem Docker é criar um arquivo
chamada **Dockerfile** esse arquivo contém todas as informações necessárias
para criamos nossa estrutura de diretório que nossa imagem docker vai conter.

O simples fato de termos isso em um arquivo já nos garante um princípio bastante
legal chamado Infrastructure as Code.

Vamos dar uma olhada nesse arquivo

```dockerfile
FROM openjdk:11

...continua

```
A palavra **FROM** indica que nossa imagem utiliza como base a imagem do openjdk
todos dockerfiles devem ter essa instrução.
Isso vai nos ajudar, porque perceba, não precisamos declarar a instalação
do java, essa imagem já vem previamente configurada!!!! 

No nosso segundo passo, vamos informar o caminho do nosso jar como argumento
```dockerfile
FROM openjdk:11
ARG JAR_FILE=target/<seu_projeto>.jar

...continua

```
**ARG** serve como indicação de varíavel dentro do processo de criação da imagem, uma espécie
de varíavel de ambiente dentro do processo de build da imagem.

**Nota importante**: Perceba que nosso artefato, ou jar já foi previamente construído,
nesse modelo a imagem não é responsável pela criação do artefato jar. Fizemos apenas a utilização
do mesmo

Agora, no terceiro passo precisamos copiar nosso jar para dentro da nossa imagem, 
perceba que nossa imagem é uma estrutura de arquivos separada.
Vamos fazer isso!!!

```dockerfile
FROM openjdk:11
ARG JAR_FILE=target/<seu_projeto>.jar
COPY ${JAR_FILE} app.jar

...continua

```
Nota a inclusão do comando **COPY**, esse comando é capaz de copiar o artefato para
dentro da imagem, e renomeá-lo para ficar mais fácil utilização.

Nosso último passo agora!!! Nosso artefato esta dentro da imagem, agora precisamos encontrar 
um comando que instrua o docker em como subir nossa aplicação 

Vamos ver como podemos fazer isso!!!

```dockerfile
FROM openjdk:11
ARG JAR_FILE=target/<seu_projeto>.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

O comando ENTRYPOINT permite que a gente instrua como nossa aplicação vai rodar, no caso
o nosso jar.

Legal, veja que instruímos o docker em como criar nossa imagem.

# Informações de suporte

* Talvez você esta se perguntando, porque criar um arquivo?? [Nesse link tem um detalhamento 
sobre o que é Infrastructure as Code](iac-immutable-infrastructure.md)
* Ou ainda em algum momento você pode ter pensado "Quero aprender mais sobre Infrastructure as a Code"
  * [Aqui você encontra uma explicação](https://www.hashicorp.com/resources/what-is-infrastructure-as-code/) um pouco mais histórica da necessidade de versionarmos nosso código fonte
  * Se ainda você quer se aprofundar ainda mais [esse link vai resolver muitas dúvidas](https://www.ibm.com/cloud/learn/infrastructure-as-code)
* Talvez você possa querer instalar o docker na sua máquina. [Esse link pode te ajudar com isso!!!](https://docs.docker.com/get-docker/)  
* Se você ficou em dúvida em como podemos utilizar o comando FROM, [esse link tem algumas informações que podem
  te ajudar a compreender melhor os detalhes](https://docs.docker.com/engine/reference/builder/#from)
* Se você acha que precisa de mais detalhamentos sobre o comando ARG, [esse link é a referência pra isso!!](https://docs.docker.com/engine/reference/builder/#arg)  
* Talvez você pode estar se questionando em quais informações o COPY é capaz de copiar. [A documentação pode ser um caminho para sanar sua dúvida](https://docs.docker.com/engine/reference/builder/#copy)
* Em algum momento você pode ter dúvidas sobre a real necessidade do ENTRYPOINT. [Aqui você pode ficar por
  dentro do comando](https://docs.docker.com/engine/reference/builder/#entrypoint)





