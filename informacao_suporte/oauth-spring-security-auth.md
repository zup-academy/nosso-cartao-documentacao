# Bloqueando nossas requisições com base em tokens!

Nosso objetivo é indicar para o Spring Security o que deve ser avaliado para permitir ou não o processamento da requisição 
de acordo com o token passado em nosso sistema.

Essa prática é chamada de Autorização, perceba que com as credenciais em mãos _(Autenticação)_, aqui
nossos tokens, vamos aplicar algum conjunto de regras e então decidir negar ou permitir 
a requisição

```java
@Configuration
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests(authorizeRequests ->
                        authorizeRequests
                                .antMatchers(HttpMethod.GET, "/api/propostas/**").hasAuthority("SCOPE_propostas:read")
                                .antMatchers(HttpMethod.GET, "/api/cartoes/**").hasAuthority("SCOPE_cartoes:read")
                                .antMatchers(HttpMethod.POST, "/api/cartoes/**").hasAuthority("SCOPE_cartoes:write")
                                .antMatchers(HttpMethod.POST, "/api/propostas/**").hasAuthority("SCOPE_propostas:write")
                                .anyRequest().authenticated()
                )
                .oauth2ResourceServer(OAuth2ResourceServerConfigurer::jwt);
    }

}
``` 

Esse método está presente na classe [WebSecurityConfigurerAdapter](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/config/annotation/web/configuration/WebSecurityConfigurerAdapter.html) do Spring, esta classe basicamente
permite que façamos algumas configurações relacionadas a segurança no framework, perceba que declaramos uma série de configurações relacionadas a **paths** das nossas APIs e suas
credenciais necessárias para acessá-las.

Vamos selecionar um exemplo:

```java
.antMatchers(HttpMethod.GET, "/api/propostas/**").hasAuthority("SCOPE_propostas:read")
```

Note que para as nossas APIs prefixadas por _/api/propostas/**_ , aqui podemos usar wildcards, devem ser protegidas por uma
regra, o token repassado deve conter a claim _SCOPE_propostas:read_, caso contrário a requisição será negada.

Uma informação bastante importante aqui as claims do token JWT se tornam Roles no Spring Security!!

Outra informação importante: você não precisa necessariamente usar os **scopes** do seu JWT, se você utilizar
alguma custom claim para validá-lo, não há nenhuma restrição em usar uma claim específica
utilizamos scope por acharmos mais indicado para nosso caso, mas atente-se às necessidades
do seu projeto.

Pronto e agora, que tal colocar isso em prática no seu projeto?

# Informação de Suporte

* Talvez seja a primeira vez que você tenha se deparado com o termo **Autorização**, esse termo
é muito importante quando falamos em segurança de software. [Aqui você pode encontrar uma boa
definição sobre Autorização](https://auth0.com/docs/authorization)

* O material anterior detalha muito bem sobre o processo de Autorização, mas é **muito** importante
que consigamos entender a diferença entre **Autenticação** e **Autorização** isso vai nos ajudar a
aplicar um modelo de segurança mais efetivo. [Esse link pode ter ajudar muito com isso](https://auth0.com/docs/authorization/authentication-and-authorization)

* Talvez você possa estar se perguntando "Mas o que é um scope no JWT?". [Esse link pode ter dar uma breve introdução sobre o tema](https://oauth.net/2/scope/) 

  * Ou se você prefere dar uma revisada na RFC, [este link vai te levar para la!!](https://tools.ietf.org/html/rfc6749#section-3.3) 
