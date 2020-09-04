# Controllers 100% coesos

A primeira coisa é entender o significado da palavra coesão. Existem algumas métricas disponíveis para avaliar coesão, a que eu utilizo como base aqui é uma chamada Tight and Loose Class Cohesion(https://www.aivosto.com/project/help/pm-oo-cohesion.html#TCC_LCC). Não dá para aplicá-la exatamente igual o sugerido, já que um controller não é bem uma classe no sentido puro da palavra.

Um controller é apenas um recipiente de rotas que representam os endpoints expostos nas aplicações. Ele não mantém estado da aplicação e seus atributos deveriam ser, na verdade, variáveis locais de seus métodos. Uma rota é uma função, que recebe uma entrada e gera uma saída. Pela definição do artigo Tipos Abstratos de Dados(https://dl.acm.org/doi/pdf/10.1145/942572.807045) ela é uma função abstrata. O problema é que linguagens como Java e C# nos obrigam a escrever classes para que seja possível declarar funções(métodos estáticos). E os frameworks se apoiam nisso. Em vez de declararmos variáveis locais, declaramos atributos e recebemos seus valores injetados pelo framework. **Podemos dizer que um controller é uma classe com atributos de dependência.**

Dado esse cenário, a minha sugestão é que todo método de um controller use todos os atributos declarados. Além disso a carga intrínseca dele não deveria passar de 7 pontos. O resultado dessa combinação é que você vai ter controllers enxutos e que não ultrapassam o limite da memória de trabalho(https://medium.com/@albertosouza_47783/um-outro-olhar-sobre-complexidade-de-c%C3%B3digo-16370f9f9c80).

O tradeoff é que você vai ter mais classes que representam controllers do que você tem atualmente. Na minha opinião isso não é um problema. Inclusive controllers inflados foi justamente um problema encontrado por Aniche(http://pure.tudelft.nl/ws/files/12555765/TUD_SERG_2016_023.pdf) numa pesquisa que ele fez em cima de várias aplicações web encontradas no github. 

É importante lembrar que mais arquivos só são um problema se eles não estiverem distribuindo de maneira equilibrada a carga cognitiva pelo sistema.

Por fim, um controller escrito usando um framework interessante, já abstrai toda infra http para você.

Agora você tem um cenário onde ele é enxuto e super específico. A soma disso é que na minha opinião você pode fundir em vários momentos a ideia de Application Service com Domain Service(Domain Service Controller?) e chegar em um código parecido com esse:

```java
    @RestController
    public class RetornoPagamentoPagSeguroController {
        @Autowired
        private CompraRepository compraRepository;
        @Autowired
        private PagamentoRepository pagamentoRepository;
        @Autowired
        private ApplicationEventPublisher applicationEventPublisher;
            
        @InitBinder
        public void initBinder(WebDataBinder dataBinder) {
            dataBinder.addValidators(new   VerificaSeCompraJaEstaConcluidaValidator(compraRepository));
        }
        @PostMapping(value = {"/api/retornopagamento/{compraId}/pagseguro"})
        @Transactional
        public void processaRetorno(@PathVariable("compraId") Long compraId, @Valid RetornoPagamentoPagSeguroRequest retornoPagamentoPagSeguroRequest, UriComponentsBuilder uriComponentsBuilder) {
            Compra compra = FindById.executa(compraId, compraRepository);     
            Pagamento pagamento = retornoPagamentoPagSeguroRequest.criaPagamento(compra);

            pagamentoRepository.save(pagamento);
            compraRepository.save(compra);
            applicationEventPublisher.publishEvent(new NovoPagamentoEvent(pagamento, uriComponentsBuilder));
        }
    }
```

Dado a minha sugestão de que o único acoplamento que devemos levar em consideração é o feito com classes criadas no próprio sistema, temos a seguinte conta de carga intrínseca aqui:

* +1 CompraRepository;
* +1 PagamentoRepository;
* +1 VerificaSeCompraJaEstaConcluidaValidator;
+ +1 RetornoPagamentoPagSeguroRequest;
* +1 Compra;
* +1 FindById;
* +1 Pagamento;
* +1 NovoPagamentoEvent;

Temos 8 pontos de carga intrínseca. Ultrapassa em 1 ponto a sugestão para um Domain service controller :). O que você faria? E perceba que você já fez tudo necessário para a execução da lógica de negócio também.

Eu sugiro a carga do Domain service controller ficar em 7 justamente porque ele está na borda mais externa da aplicação e, por ser um local onde as pessoas começam a olhar um código, deveria ser mais fácil de entender. 

Claro que você pode ser mais restritivo e baixar essa pontuação se achar interessante, experimente. Um detalhe legal é que só passamos de 7 pontos porque o foi decidido usar uma abstração chamada FindBy para isolar o tratamento do retorno Opcional da busca pelo id da Compra.

Você ganhou controllers coesos, com carga cognitiva baixa e que tem uma régua clara para review de código. Inclusive que pode ser automatizada. Se a carga intrínseca passar de 7, você tenta distribuir :). Vou dar um exemplo para esse de cima:

```java
    @RestController
    public class RetornoPagamentoPagSeguroController {
        @PersistenceContext
        private EntityManager manager;
        @Autowired
        private ApplicationEventPublisher applicationEventPublisher;

        @InitBinder 
        public void initBinder(WebDataBinder dataBinder) {  
            dataBinder.  addValidators(new VerificaSeCompraJaEstaConcluidaValidator(compraRepository));
        }

        @PostMapping(value = {“/api/retorno-pagamento/{compraId}/pagseguro”})
        @Transactional
        public void processaRetorno(@PathVariable(“compraId”) Long  compraId, @Valid RetornoPagamentoPagSeguroRequest retornoPagamentoPagSeguroRequest, UriComponentsBuilder uriComponentsBuilder) {
            Compra compra = manager.find(compraId,Compra.class);
            Pagamento pagamento = retornoPagamentoPagSeguroRequest.criaPagamento(compra);

            manager.persist(pagamento);
            applicationEventPublisher.publishEvent(new NovoPagamentoEvent(this, pagamento, uriComponentsBuilder));
        }
    }
```
Usei o EntityManager da JPA direto e ainda tirei uma linha de save que não precisava. Agora, se fizermos a mesma conta:

* +1 VerificaSeCompraJaEstaConcluidaValidator;
+ +1 RetornoPagamentoPagSeguroRequest;
* +1 Compra;
* +1 Pagamento;
* +1 NovoPagamentoEvent;

Saímos de 8 para 5 sem criar novos arquivos, códigos etc. Usei o EntityManager direto no nosso mais novo Domain service controller? Usei, e daí :)?

E se eu puder processar compras através de outras entradas do sistema? Adapte o código :). Quando um sistema cresce, pouco importa se a arquitetura é monolítica ou distribuída, você vai perdendo o controle do que está pronto ou não. No fim, você não precisa ter medo de mudança, basta que ela seja mais fácil de ser realizada. Você agora tem um fluxo com carga intrínseca baixa e que pode ser mais fatiado em caso de necessidade.