# Criando Web Services Clients com Feign

Precisamos com certa frequência criar diferentes web service clients, nosso serviço,
na maioria das vezes necessitam se comunicar entre eles. 

Podemos encontrar alguns padrões no processo de criação desses clientes, envolvem
mapeamento de objetos de entrada, saída e configurações de URI como Path Params e Query Params.
O projeto OpenFeign pode nos ajudar nessa geração, já que podemos identificar um padrão na escrita 
desses clientes.

Para integrar o OpenFeign no sistema existe um projeto chamado Spring Cloud OpenFeign.
Então vamos ver como podemos usá-lo.

## Configurando a dependência do projeto

Nosso primeiro passo é incluir a dependência da biblioteca no nosso projeto

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```
Note que a dependência é do projeto "guarda-chuva" [Spring Cloud](https://spring.io/projects/spring-cloud)

```java
@EnableFeignClients
``` 
Essa anotação indica para o Spring Framework que nosso projeto vai utilizar a configuração
de clientes web services dinâmicas.
 
Ok!! Dependência adicionada agora podemos começar definir nosso cliente wevb service. O
projeto OpenFeign utiliza interfaces para definir nossas operações com serviço web, depois de verificar a
documentação podemos começar a construir nosso cliente.


```java
@FeignClient("cartoes")
public interface CartoesClient {
    
    @RequestMapping(method = RequestMethod.GET, value = "/cartoes")
    List<Cartao> cartoes();
    
}
```

@FeignClient define o nome do cliente que estamos criando, isso é bastante importante porque isso pode ser utilizado
em regras de balanceamento de carga

Logo depois, definimos nossa operação cartoes(), mas tem algumas coisinhas importantes logo acima da nossa operação
@RequestMapping que indica alguma configurações que podemos realizar.

Quando vamos chamar uma operação precisamos saber a URI dessa operação no servidor e também precisamos saber o método HTTP
que essa operação chama. Com @RequestMapping conseguimos resolver esse problema!!!!

Legal, nosso cliente web service estamos criando agora podemos chamar nosso serviço externo!!!

## Lidando com erros

Talvez esteja pensando e quando ocorrer erro na faixa do 4xx e 5xx, como lidar?

Quando ocorre erro na faixa do 4xx ou 5xx o Feign lança uma exceção específica para cada família de status do HTTP, 
como por exemplo:

- [FeignClientException](https://javadoc.io/static/io.github.openfeign/feign-core/10.7.0/feign/FeignException.FeignClientException.html): Em caso de erro 4xx
- [FeignServerException](https://javadoc.io/static/io.github.openfeign/feign-core/10.7.0/feign/FeignException.FeignServerException.html): Em caso de erro 5xx

Se não deseja segmentar por faixa de status code, não tem problema, basta tratar a exceção [FeignException](https://javadoc.io/static/io.github.openfeign/feign-core/10.7.0/feign/FeignException.html).

Pronto! Agora sabemos lidar com erro!

Se quiser obter a resposta do erro, como por exemplo o body, existe um método para isto o [content()](https://javadoc.io/static/io.github.openfeign/feign-core/10.7.0/feign/FeignException.html#content--);

Pronto! Estamos mais preparados para lidar com os cenários da Zup!

## Informações de suporte

- Se você tem alguma dúvida do que é interface java [esse link](https://www.caelum.com.br/apostila-java-orientacao-objetos/interfaces) pode te ajudar, isso é bem importante para
conseguirmos entender o OpenFeign

- Talvez você esteja em dúvida qual operação e verbo HTTP usar, [nesse caso esse conteúdo vai te ajudar a sanar essa dúvida](../informacao_suporte/rest-get.md)

- Não entendi muito bem a parte de documentação, por que eu deveria olhar ela??? [Este link tem algumas explicações interessantes sobre o modelo de documentção que estamos utilizando]((http://spec.openapis.org/oas/v3.0.3))

- Talvez você queira explorar mais as funcionalidadesdo Feign, [aqui você encontra o código fonte e a documentação](https://github.com/OpenFeign/feign) 

- Se você ficou com dúvida sobre como usar URI, [este link vai resolver seu problema!!!](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Basico_sobre_HTTP/Identifying_resources_on_the_Web)

- Quero saber os detalhes da ferramenta. [Aqui você encontra a documentação completa](https://cloud.spring.io/spring-cloud-openfeign/reference/html/)

- O **Spring Cloud** conta com vários projetos que nos ajudam a construir sistemas distribuídos
se você tem interesse nesse modelo de arquitetura, [aqui você pode encontrar o índice com todos os projetos](- Se você)


