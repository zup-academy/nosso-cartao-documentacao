# Gerando projeto com Maven Archetype

Nesse tutorial vamos aprender como gerar um projeto utilizando o [Maven Archetype](https://maven.apache.org/archetype/index.html), primeiro precisamos saber o 
que é [Maven](https://maven.apache.org/what-is-maven.html).

## [Maven](https://maven.apache.org/what-is-maven.html)

[Maven](https://maven.apache.org/what-is-maven.html) é uma ferramenta de gerenciamento e automação 
de construção (build) de projetos. Entretanto, por fornecer diversas funcionalidades adicionais através do uso de 
plugins e estimular o emprego de melhores práticas de organização, desenvolvimento e manutenção de projetos, é 
muito mais do que apenas uma ferramenta auxiliar!

Já sabemos o que é [Maven](https://maven.apache.org/what-is-maven.html), bora falar de Archetype?

## [Maven Archetype](https://maven.apache.org/archetype/index.html)

[Maven Archetype](https://maven.apache.org/archetype/index.html) tem como objetivo catalogar vários padrões de projeto, 
como por exemplo:

[maven-archetype-quickstart](https://maven.apache.org/archetypes/maven-archetype-quickstart/): Archetype para gerar um 
projeto na estrutura do Maven, conforme imagem abaixo:

![alt text](../images/maven-001.png "maven-archetype-quickstart")

Para saber quais são os outros Archetype, acesse o [catálogo](https://maven.apache.org/archetypes).

#### Agora que sabemos os conceitos, bora colocar em prática?

Para gerar nosso projeto, iremos utilizar o [maven-archetype-quickstart](https://maven.apache.org/archetypes/maven-archetype-quickstart/) 
para tal precisamos instalar o [Maven](https://maven.apache.org/what-is-maven.html) em nosso ambiente.

- Ops, não tenho Maven instalado, não tem problema, [aqui você encontra como fazer isto!](https://maven.apache.org/install.html)

Agora que tudo está ok, vamos começar?

1º Acesse o terminal do seu sistema operacional

2º Execute o comando abaixo:

```
mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes \
-DarchetypeArtifactId=maven-archetype-quickstart \
-DarchetypeVersion=1.4
```

3º Escolha **groupId**, como por exemplo: br.com.zup

4º Escolha o **artifactId**, no qual é o nome do seu projeto, como por exemplo: nosso-cartão-proposta

5º Escolha o **version**, se necessário.

6º Escolha o **package**, se necessário.

**Pronto! Temos um projeto, bora começar a codificar?**
