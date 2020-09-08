# Habilitando Secrets no Vault

Precisamos armazenar nossas credenciais ou strings que contém valores sensíveis dentro de um
"cofre", algum lugar que estes dados seja passível de algum modelo de criptografia.

O Hashicorp Vault possui uma feature que pode nos ajudar com isso, essa feature é chamada
de **Secret Engine**.

Esse engine é capaz de armazenar valores, utilizando conceito de chave valor. Então
isso se traduz uma chave **"secret/minhaapp"** tem um valor, esse valor pode ser composto de uma 
ou mais strings.

Então o primeiro passo é se conectar com o vault, aqui recomendamos que você se conecte via bash no 
próprio container do vault, não há problema quando estamos em fase de desenvolvimento.

Uma vez conectado precisamos garantir que a feature de secret engine está habilitada, podemos fazer
isso via o seguinte comando:

```shell script
vault secrets enable -path=secret/ kv
```

Feito isso estamos apto à guardar nossos "segredos" lá, então vamos fazer isso

```shell script
vault kv put secret/spring-vault-sidecar APP_DATA=spring ENV_VAR_DATA=hello
``` 

Pronto, seus segredos estão guardados dentro de um cofre!!!! rs..

Agora suas aplicações podem se conectar e consumir os valores sensíveis quando necessário!!!

E que tal um desafio???? Tem um jeito ainda mais seguro de proteger seus segredos
que tal dar uma olhada nas "policies" do vault. [Esse link dá uma boa explicação](https://www.vaultproject.io/docs/concepts/policies)

Tente aplicar uma política para que somente sua aplicação possa acessar determinada secret!!! Depois é claro
nos conte o resultado!!!

## Informações de suporte

* Você pode estar se perguntando, "o que é vault??", [este link tem algumas informações importantes](https://www.vaultproject.io/)

* Talvez você gostou da idéia de guardar dados criptografados dentro de um cofre, [esse link explica
com alguns detalhes de implementação o ciclo de vida de uma secret](https://www.vaultproject.io/docs/secrets)

* Caso você tenha dificuldade em se conectar com o vault, [esse link pode te ajudar no processo de login](https://www.vaultproject.io/docs/commands/login)

* Talvez você esteja com dificuldade em habilitar a secret engine, [este link pode te ajudar](https://www.vaultproject.io/docs/commands/secrets/enable)