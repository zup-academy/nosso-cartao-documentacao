# Rodando nossa imagem docker

Uma imagem docker é como se fosse um "template", ela tem a estrutura de diretórios e arquivos necessários
para rodar um container, um detalhe bem importante é que a imagem é estática, ou seja não há modificações
do conteúdo.

Depois que escolhermos a imagem desejada, estamos aptos a criar containers à partir dela. Para isso podemos
usar o comando **docker run**, na prática esse comando vai rodar um container usando premissas de containeirização
com seu próprio filesystem, sua rede e processo separado do host.  

Então já que temos nossa imagem é hora de rodar nosso container!!!

```shell script
docker container run -d -p 8080:8080 zupacademy/proposta --name proposta
```

Vamos entender um pouquinho desse comando. A primeira parte do comando **docker container run** indica que estamos chamando
a docker engine para rodar nosso container. Logo depois temos a flag **-d* que instrui a engine para rodar em _background_
e liberar nossa linha de comando.
Logo depois temos outra flag, essa é bastante importante e é relacionada a redes. A flag **-p 8080:8080** indica que gostaríamos
que a porta _8080_ do container seja "atachada" a porta _8080_ da nossa máquina. Isso é bastante comum em ambientes de desenvolvimento
para que possamos chamar nossos containers usando **localhost**.

O argumento **zupacademy/proposta** indica o nome da imagem do container. Nesse caso estamos usando um repositório público
por isso é prefixado pelo usuário, que no nosso caso é **zupacademy**.

E nosso último argumento é o nome do nosso container, normalmente utilizamos para facilitar o gerenciamento dos containers
na nossa máquina...


## Informações de suporte
* Talvez você possa estar intessado em saber mais detalhes sobre "rodar em segundo plano", 
[esse link pode te ajudar](https://docs.docker.com/engine/reference/run/#detached-vs-foreground)
* Se por algum motivo você queira explorar mais sobre sobre networking do docker, [este link pode te ajudar!!](https://docs.docker.com/network/)
  * Ou talvez você possa estar se pergutando sobre quais opções eu tenho para expor portas, [esse link da documentação pode te ajudar com isso](https://docs.docker.com/engine/reference/run/#expose-incoming-ports)
* Se você está com dúvida sobre o parâmetro **name**, [esse link pode te ajudar entender algumas coisas relacionadas a identificação do container](https://docs.docker.com/engine/reference/run/#name---name)  
Se você estiver afim de se aprofundar no comando docker container run, [aqui você encontra a documentação completa](https://docs.docker.com/engine/reference/run/)
