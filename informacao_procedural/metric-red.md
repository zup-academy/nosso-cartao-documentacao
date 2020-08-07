# Métrica tipo RED

Quando falamos de métricas, existem vários tipos de métricas para responder várias perguntas, como por exemplo:

- Métricas de infraestrutura, como por exemplo: CPU, memória, rede, etc.
- Métricas de negócio, como por exemplo: Quantidade de usuário, compras, vendas, conversão, etc.

E quando falamos de arquitetura distribuída, como por exemplo Microsserviços, existe uma boa prática denominada RED, na 
qual tem o objetivo de responder três perguntas e deve ser implementada em todos os serviços!

- **R**ate: Quantidade de solicitações, por segundo, que seus serviços estão processando.
- **E**rros: Quantidade de solicitações com falha por segundo.
- **D**uration: Quantidade de tempo que cada solicitação leva.

Ter essas métricas é extremamente importante e **recomendada** pela **Zup**, pois ajuda muito em troubleshooting de 
anomalias em nossos serviços, como por exemplo!

Clientes estão reclamando que está muito lento a Transferência de TED e infelizmente o time de sustentação não consegue 
encontrar o problema, pois não tem métricas!

Foi solicitado para o time de desenvolvimento implementar as métricas RED e logo após a sua implementação e implantação 
em produção, ficou claro o problema!

Por conta do COVID-19 a quantidade de solicitações por segundo cresceu muito e os serviços provisionados não conseguem 
suportar tal carga, ocasionando dois problemas:

- Muitas requisições com falha por segundo, ocasionando uma péssima experiência para o usuário \ cliente.
- Muitas requisições com tempo alto, ocasionando uma péssima experiência para o usuário \ cliente, pois ele conseguiu 
fazer sua transferência, porém levou-se muito tempo!

Por conta desse episódio e a demora na correção, devido falta de métrica, alguns clientes migraram de Banco!

# Informação de Suporte

Gostaria de saber mais sobre Métricas do tipo RED? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/#xref_monitoring_golden-signals)

Está em dúvida sobre o que é Métrica? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/metric.md)


https://www.weave.works/blog/the-red-method-key-metrics-for-microservices-architecture/

https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/#xref_monitoring_golden-signals