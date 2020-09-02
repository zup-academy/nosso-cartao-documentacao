# Como utilizar Vault no Spring?

Nos materiais anteriores a gente viu o conceito e a importância sobre Vault!

Talvez esteja se perguntando, como utilizar Vault no Spring?

Não se preocupe, neste tutorial, iremos de forma simples, fornecer todas as informações para configurar o Vault no Spring!

Vamos começar?

Como todo framework o Spring tenta abstrair o máximo a complexidade para nós desenvolvedores(as) e para que isso seja 
necessário precisamos adicionar algumas dependências que contém as configurações automáticas!

Primeiro, precisamos adicionar algumas configurações no nosso `pom.xml`, conforme abaixo:

```xml
<properties>
    <!-- Omitidas outras propriedades -->
     <spring-cloud.version>Hoxton.SR8</spring-cloud.version>
</properties>
```

Agora que adicionamos as propriedades, precisamos adicionar um gerenciador de dependência, conforme abaixo:

```xml
<dependencyManagement>

    <dependencies>

        <!-- Omitidas outras dependências -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>${spring-cloud.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>

    </dependencies>

</dependencyManagement>
```

Gostaria de saber mais sobre Dependency Management no Maven? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)

Agora que está tudo configurado (Propriedades e Dependency Management), precisamos adicionar a seguinte dependência:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-vault-config</artifactId>
    </dependency>
</dependencies>
```

Você deve estar pensando, está tudo configurado? Infelizmente falta apenas uma configuração!

Agora que está tudo configurado, precisamos adicionar as seguintes propriedades no arquivo `bootstrap.properties` que 
se encontra na pasta `/src/main/resources/`, conforme abaixo:

```properties
# Vault Enabled - Must be true in production
spring.cloud.vault.enabled=${VAULT_ENABLED:true}

# Vault Address
spring.cloud.vault.port=${VAULT_PORT:8200}
spring.cloud.vault.host=${VAULT_HOST:localhost}

# Vault secret name - Spring will use the prefix secret e.g: secret/my-secret
spring.cloud.vault.application-name=${VAULT_SECRET_NAME:my-secret}

# Vault token - Must be one per application context
spring.cloud.vault.token=${VAULT_TOKEN:13d5a277-23d8-4c59-bb23-5c214883112f}

# Vault Scheme - http (local development) or https (production)
spring.cloud.vault.scheme=${VAULT_SCHEME:http}
```

> Caso o arquivo `bootstrap.properties` não exista, crie o mesmo na pasta `/src/main/resources/`!

Pronto! Agora sim está tudo configurado! Vamos testar?

Para testar cadastre algumas propriedades no arquivo `application.properties`, como por exemplo:

```properties
database.username="Vault irá substituir esse valor"
database.password="Vault irá substituir esse valor"
database.platform=${DATABASE_PLATFORM:MySQL}
```

Agora cadastre as mesmas propriedades no `Vault` de acordo com o `secret` configurado na propriedade 
`spring.cloud.vault.application-name` que se encontra no arquivo `bootstrap.properties`, conforme exemplo abaixo:

```shell script
$ vault kv put secret/my-secret database.username=luramarchanjo database.password=1234567890
````

Inicie sua aplicação conforme desejar ou utilizando o comando `mvn clean spring-boot:run` e verifique se as 
propriedades cadastradas no Vault foram carregadas com os valores corretos!

Deu tudo certo? Demais né!

Em tempo de inicialização o Spring irá carregar as propriedades cadastradas no `Vault` na secret `my-secret` e irá 
substituir os valores, caso as propriedades existam no arquivo `application.properties`, pelo valor configurado no `Vault`.

Caso a propriedade esteja mapeada no arquivo `application.properties` e não no `Vault` será considerado o valor do arquivo 
ou da variável de ambiente, caso configurado, como por exemplo, a propriedade `database.platform` na qual não foi 
configurada no `Vault`, portanto, o Spring irá considerar o valor `MySQL` caso a variável de ambiente `DATABASE_PLATFORM` 
não existir!

# Informação de Suporte

Quer saber mais sobre Spring Vault? Acesse o [link!](https://spring.io/projects/spring-vault#overview)

Quer saber mais sobre Vault? Acesse o [link!](https://www.vaultproject.io/)