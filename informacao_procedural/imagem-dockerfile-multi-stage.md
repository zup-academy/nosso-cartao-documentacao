# Melhorando nossas imagens com multi-stage builds!!!

Quando pensamos em imagens, tentamos minimizar o tamanho delas.

Tente imaginar a seguinte situação, sua aplicação precisa estar apta a rodar o mais rápido possível, considerando
que algum servidor precisa realizar o download da imagem e iniciar o processo de subida da aplicação. Agora
se sua imagem tiver 1GB de tamanho, isso com certeza vai degradar o funcionamento adequado da sua aplicação.

Precisamos achar uma maneira que nos ajude a reduzir o tamanho das nossas imagens, é o multi-stage build é um caminho
para nos ajudar com isso.

E mais legal ainda, podemos rodar nossa build dentro do Docker, não precisamos nenhuma dependência na nossa máquina porque a produção 
do artefato é feita dentro do container...muito massa!!!

Então não vamos perder tempo e fazer isso acontecer!!!

```dockerfile

## Builder Image
FROM maven:3.6.3-jdk-11 AS builder
COPY src /usr/src/app/src
COPY pom.xml /usr/src/app
RUN mvn -f /usr/src/app/pom.xml clean package

## Runner Image
FROM openjdk:11
COPY --from=builder /usr/src/app/target/docker-hands-on-0.0.1-SNAPSHOT.jar /usr/app/app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/usr/app/app.jar"]

```

Opa, temos dois comandos FROM???

Perceba, que temos dois estágios na nossa build, podemos notar que no primeiro estágio utilizamos o maven como base. O maven é utilizado
para realizar a build da nossa aplicação e produzir nosso artefato, dentro desse estágio é artefato produzido.

Podemos criar um **alias** para esse estágio, no caso usamos o nome _builder_.

Um detalhe bastante importante é que nossa aplicação não precisa de maven para rodar em produção, para nossa aplicação rodar precisamos somente
do JRE, note que o maven na fase de runtime se torna um overhead no sistema de arquivos, não precisamos dele para rodar. Com isso introduzimos
nosso segundo **FROM** que contém somente openjdk.

Note que no comando **COPY** usando a flag **--from** e indicamos o caminho de qual arquivos queremos copiar, no nosso caso queremos copiar o artefato produzido
no primeiro estágio. Indicamos um caminho que desejamos ser mais adequado.

Por fim, declaramos que nossa aplicação expõe nossos serviços na porta _8080_.

Esta técnica reduz consideravelmente o tamanho da sua imagem, é atualmente é o modelo mais adequado para adotarmos. 
   
## Informações de suporte

* Talvez você possa querer instalar o docker na sua máquina. [Esse link pode te ajudar com isso!!!](https://docs.docker.com/get-docker/)

* Se em algum momento você pensou em entender em mais detalhes o padrão multi-stage. [Esse link vai te ajudar muito.](https://docs.docker.com/develop/develop-images/multistage-build/) 
  
  * Aqui você pode encontrar dicas de utilização para criação de [multi-stage builds](https://www.docker.com/blog/advanced-dockerfiles-faster-builds-and-smaller-images-using-buildkit-and-multistage-builds/)

* Se você ficou em dúvida em como podemos utilizar o comando FROM, [esse link tem algumas informações que podem
  te ajudar a compreender melhor os detalhes](https://docs.docker.com/engine/reference/builder/#from)

* Se você acha que precisa de mais detalhamentos sobre o comando ARG, [esse link é a referência pra isso!!](https://docs.docker.com/engine/reference/builder/#arg)  

* Talvez você pode estar se questionando em quais informações o COPY é capaz de copiar. [A documentação pode ser um caminho para sanar sua dúvida](https://docs.docker.com/engine/reference/builder/#copy)

* Em algum momento você pode ter dúvidas sobre a real necessidade do ENTRYPOINT. [Aqui você pode ficar por
  dentro do comando](https://docs.docker.com/engine/reference/builder/#entrypoint)