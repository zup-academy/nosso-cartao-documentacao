# Métrica tipo USE

Quando falamos de métricas, existem vários tipos de métricas para responder várias perguntas, como por exemplo:

- Métricas de infraestrutura, como por exemplo: CPU, memória, rede, etc.
- Métricas de negócio, como por exemplo: Quantidade de usuário, compras, vendas, conversão, etc.

E quando falamos de arquitetura distribuída, como por exemplo Microsserviços, existe uma boa prática denominada USE, na qual tem o objetivo de responder três perguntas e deve ser implementada em todos os serviços!


- **U**tilization: A média de tempo que o recurso está sendo utilizado.
- **S**aturation: O grau em que o recurso tem trabalho extra que não pode atender.
- **E**rror: Quantidade de falhas no recurso.

Ter essas métricas é extremamente importante e **recomendada** pela **Zup**, pois ajuda muito em troubleshooting de 
anomalias em nossos serviços, como por exemplo!

Clientes estão reclamando que está muito lento o envio de email e infelizmente o time de sustentação não consegue encontrar o problema, pois não tem métricas!

Foi solicitado para o time de desenvolvimento implementar as métricas USE e logo após a sua implementação e implantação em produção, ficou claro o problema!

Por conta do aumento de envios de email os serviços provisionados não conseguem suportar tal carga:


- Métrica de **U**tilization mostrou que o CPU em média utilizado nos últimos dias foi de **95%**, ou seja, o recurso 
está em constante estresse!

- Métrica de **S**aturation mostrou que a fila de envio de email está em constante espera, ou seja, explica o motivo da 
demora no envio dos emails.

- Métrica de **E**rror mostrou que por conta da demora de processamento da fila, muitos e-mails são descartados devido a 
regra de expiração (timeout).

Por causa desse episódio e a demora na correção, devido à falta de métrica, alguns clientes migraram de servidor de email!

Super interessante, né? Como a falta de métricas impacta diretamente no software /produto!

Lembrando que é apenas um exemplo de como as métricas podem ajudar a manter a qualidade do seu software/ produto!


# Informação de Suporte

Gostaria de saber mais sobre Métricas do tipo USE? [Aqui tem uma explicação do que entendemos que você deve considerar!](http://www.brendangregg.com/usemethod.html)

Está em dúvida sobre o que é Métrica? [Aqui tem uma explicação do que entendemos que você deve considerar!](../informacao_procedural/metric.md)
