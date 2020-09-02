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
do Java, essa imagem já vem previamente configurada!

No nosso segundo passo, vamos informar o caminho do nosso Jar como argumento

```dockerfile
FROM openjdk:11
ARG JAR_FILE=target/<seu_projeto>.jar

...continua
```

**ARG** serve como indicação de variável dentro do processo de criação da imagem, uma espécie
de variável de ambiente dentro do processo de build da imagem.

**Nota importante**: Perceba que nosso artefato ou jar já foi previamente construído,
nesse modelo a imagem não é responsável pela criação do artefato jar. Fizemos apenas a utilização
do mesmo.

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
dentro da imagem e renomeá-lo para ficar mais fácil utilização.

Nosso último passo agora! Nosso artefato está dentro da imagem, agora precisamos encontrar 
um comando que instrua o docker em como iniciar nossa aplicação.

Vamos ver como podemos fazer isso!

```dockerfile
FROM openjdk:11
ARG JAR_FILE=target/<seu_projeto>.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

O comando **ENTRYPOINT** permite que a gente instrua como nossa aplicação vai rodar, no caso
o nosso jar.

Legal, veja que instruímos o docker em como criar nossa imagem.

Eba! Tudo está configurado! Vamos gerar nossa imagem?

Primeiro, precisamos gerar nosso jar, para isso, execute o comando abaixo:

```shell script
mvn clean package
```

Eba! Nosso jar foi gerado! Vamos gerar nossa imagem?

Para isso, escrevemos um [material específico para você!](comando-criacao-imagem-docker.md)

# Informações de suporte

* Talvez esteja se perguntando, porque criar um arquivo denominado Dockerfile? [Aqui tem uma explicação do que entendemos que você deve considerar!](iac-immutable-infrastructure.md)

* Talvez esteja se perguntando, como instalar Docker? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://docs.docker.com/get-docker/)  

* Gostaria de saber mais sobre o comando **FROM**? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://docs.docker.com/engine/reference/builder/#from)

* Gostaria de saber mais sobre o comando **ARG**? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://docs.docker.com/engine/reference/builder/#arg)  

* Gostaria de saber mais sobre o comando **COPY**? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://docs.docker.com/engine/reference/builder/#copy)

* Gostaria de saber mais sobre o comando **ENTRYPOINT**? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://docs.docker.com/engine/reference/builder/#entrypoint)

* Gostaria de saber mais sobre Docker? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://docs.docker.com)