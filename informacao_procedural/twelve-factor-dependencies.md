# Dependências. II do 12 Factor Apps

Talvez a primeira pergunta que você tenha pensado é _Como posso deixar o que minha aplicação 
precisa explicita???_

É bem provável que você já tenha feito isso, se você usou Maven ou Gradle você já
declarou quais biblíotecas sua aplicação precisa.

Perceba que se alguém tem interesse em saber o que sua aplicação usa, basta
essa pessoa analisar seu arquivo `pom.xml` ou `build.gradle`. Nesses arquivos
as informações estão bastante explícitas.

Mas e sobre isolar as dependências??

Ferramentas como o Maven e Gradle também fazem isso, ambas são capazes
de incluir essas dependências dentro do seu artefato, ou aplicação.

Viu, como é simples!!!

## Informações de suporte

* Talvez você pode estar se perguntando o que é gradle. [Aqui você pode encontrar uma documentação detalhada](https://gradle.org/)

* Ou ainda você deve querer saber mais sobre o maven, [no site oficial você pode encontrar mais informações](https://maven.apache.org/)


