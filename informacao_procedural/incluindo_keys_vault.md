# Habilitando Secrets no Vault

Precisamos armazenar nossas credenciais ou strings que contém valores sensíveis dentro de um
"cofre", algum lugar que estes dados seja passível de algum modelo de criptografia.

O Hashicorp Vault possui uma feature que pode nos ajudar com isso, essa feature é chamada
de **Secret Engine**.

Esse engine é capaz de armazenar valores, utilizando conceito de chave valor. Então
isso se traduz uma chave **"secret/minhaapp"** tem um valor, esse valor pode ser composto de uma 
ou mais strings.

Então o primeiro passo é se conectar com o Vault, aqui recomendamos que você se conecte via bash no 
próprio container do Vault, não há problema quando estamos em fase de desenvolvimento.

Uma vez conectado precisamos garantir que a feature de secret engine está habilitada, podemos fazer
isso via o seguinte comando:

```shell script
vault secrets enable -path=secret/ kv
```

Feito isso estamos apto à guardar nossos "segredos" lá, então vamos fazer isso:

```shell script
vault kv put secret/spring-vault-sidecar APP_DATA=spring ENV_VAR_DATA=hello
``` 

Pronto, seus segredos estão guardados dentro de um cofre!

Agora suas aplicações podem se conectar e consumir os valores sensíveis quando necessário!

E que tal um desafio? Tem um jeito ainda mais seguro de proteger seus segredos
que tal dar uma olhada nas "policies" do Vault. [Esse link dá uma boa explicação!](https://www.vaultproject.io/docs/concepts/policies)

Tente aplicar uma política para que somente sua aplicação possa acessar determinada secret! Depois é claro
nos conte o resultado!

## Docker

Está executando o Vault no Docker e gostaria de executar os comandos? Não tem problema, logo abaixo tem um exemplo 
de como fazer isso!

```shell script
$ echo "Syntax"
$ docker exec -it <CONTAINER-NAME> <COMMAND>

$ echo "Example"
$ docker exec -it compose_vault_1 vault secrets list
```

Demais né! Agora você consegue executar comandos diretamente dentro do container!

## Docker compose

Está executando o Vault no Docker Compose e gostaria de executar os comandos? Não tem problema, logo abaixo tem um exemplo 
de como fazer isso!

```shell script
$ echo "Syntax"
$ docker-compose -f <DOCKER-COMPOSE-FILE>.yaml exec <CONTAINER-NAME> <COMMAND>

$ echo "Example"
$ docker-compose -f compose/nosso_cartao.yaml exec vault vault secrets list
```

Demais né! Agora você consegue executar comandos diretamente dentro do container!

## Informações de suporte

* Está em dúvida sobre o que é Vault? Não se preocupe! [Aqui tem uma explicação do que entendemos que você deve considerar!](https://www.vaultproject.io/docs/what-is-vault)

* Está com dificuldade em se conectar no Vault? Não tem problema! [Aqui tem uma explicação do que entendemos que você deve considerar!](https://www.vaultproject.io/docs/commands/login)

* Está com dificuldade em habilitar o Secret Engine no Vault? Não tem problema! [Aqui tem uma explicação do que entendemos que você deve considerar!](https://www.vaultproject.io/docs/commands/secrets/enable)