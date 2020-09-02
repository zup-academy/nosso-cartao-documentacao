# Como fornecer configurações de serviços externos para minha aplicação???

Nossa aplicação precisa acessar alguns serviços externos, esses serviços externos
estão instalados em algum lugar que pode ser identificado em uma rede de computadores.

Não podemos deixar essas configurações de endereços em arquivos de configurações dentro do nosso código fonte
e também não podemos deixá-las fixas no código fonte. Temos alguns problemas nessa abordagem
- **Segurança**: algumas informações não podem ser armazenadas dentro do repositório do código fonte 
- **Imutabilidade**: Nossa aplicação é instalada em múltiplos ambientes e provavelmente esses endereços vão variar de
ambiente para ambiente.

Configurações deve ser providas pelo ambiente no qual a aplicação roda, ou seja, sua aplicação deve sempre perguntar
ao ambiente a informação que ela precisa.

Essas configurações podem variar de ambiente para ambiente, porém se o ambiente estiver essas informações
não teremos problemas ao promover nossas aplicações entre eles.

## Mas como posso resolver isso com Spring???

O Spring suporta a configuração das aplicações usando os arquivos _*.properties_ ou _*.yaml_, nesses arquivos podemos
fazer referências as varíaveis de ambiente. 

```properties
cartoes.host=${CARTOES_URL}
```

```yaml
cartoes:
  host: ${CARTOES_URL}    
```  

Veja que em ambos os casos usamos os caracteres **$** para indicar que aquela propriedade
deve ser resolvida com varíaveis de ambiente.
  

## Quero definir um valor padrão. É possível???

Sim. Vamos fazer isso então.

```properties
cartoes.host=${CARTOES_URL:http://localhost:9999/api/cartoes}
```

```yaml
cartoes:
  host: ${CARTOES_URL:http://localhost:9999/api/cartoes}    
```  

É possível notar que utilizamos **:** separando a varíavel de ambiente do valor default.  

# Dicas de Cláudio

Utilize valores default somente em contexto de desenvolvimento, essa prática não é recomendada
para ambientes produtivos.

## Informações de suporte

- Afinal o que são varíaveis de ambiente. [Aqui você pode encontrar uma ba definição](https://opensource.com/article/19/8/what-are-environment-variables)

- O Pilar III do manifesto indica a prática de configuração da aplicação. [Você pode encontrá-lo aqui](https://12factor.net/pt_br/config)

- Quer entender todos os outros pilares do 12 Factor Apps. [Aqui você encontra!!!](https://12factor.net/pt_br/)

- Minha aplicação é instalada no kubernetes. [Aqui você encontra uma explicação básica sobre isso](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/)

- Mas se você já tem um conhecimento prévio de kubernetes e quer ver como usamos varíaveis de ambiente de uma maneira mais 
eficiente. [Esse link te dará uma grande ajuda!!!](https://kubernetes.io/docs/concepts/configuration/secret/#using-secrets-as-environment-variables)  

- Minha varíavel de ambiente é segura, eu não posso armazená-la aberta, tem como resolver isso no Kubernetes.
 [Esse link vai mostrar como podemos fazer isso de maneira eficaz](https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#define-container-environment-variables-using-secret-data)