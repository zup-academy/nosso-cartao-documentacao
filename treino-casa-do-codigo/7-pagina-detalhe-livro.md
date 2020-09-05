# Exibir detalhes de um livro

### Implementação da página de detalhe

Precisamos criar uma página com as mesmas informações que encontramos na página de detalhe da Casa do Código. Aqui está a página real => https://www.casadocodigo.com.br/products/livro-spring-boot

**A ideia aqui é implementar todo código necessário para que tenhamos uma página com as mesmas informações da página de detalhe da CDC.**

### necessidades
* Ter um endpoint que em função de um id de livro retorne os detalhes necessários para montar a página.

## Restrições
* Se o id não existir é para retornar 404

## Resultado esperado

* Em caso de sucesso retorne 200 e no corpo da resposta o json necessário para que uma aplicação rodando no front consiga montar a página
* Em caso de problema retorne 500

## sobre a utilização do material de suporte aqui

Esta é uma feature que reutiliza as habilidades trabalhadas até aqui. Tente 
implementar sem o uso do material de suporte.

## informações de suporte

* É importante você lembrar que estamos trabalhando a divisão de responsabilidade pelo olhar da dificuldade de entendimento. Uma pergunta que você pode se fazer aqui é: crio uma classe nova aqui ou apenas adiciono um método em um controller existente, dado que eu respeite a carga intrínseca máxima? Lembre de conferir a ideia de [CONTROLLERS 100% COESOS](../informacao-suporte-design/controllers-100-coesos.md) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.

* [Separamos as bordas externas do sistema do seu núcleo. Não ligamos parâmetros de requisição externa com objetos de domínio diretamente, assim como não serializamos objetos de domínio para respostas de API.](../informacao-suporte-design/nao-serializamos-objetos-de-dominio-para-respostas-de-api.md)

* É normal uma mesma classe possuir mais de uma forma de exibição de seus dados no sistema. [COMO LIDAR COM ISSO?](../informacao-suporte-design/um-objeto-muitas-representacoes.md)

* Utilize um insomnia ou qualquer outra forma para verificar o endpoint

* [PEGUE CADA UMA DAS CLASSES QUE VOCÊ CRIOU E REALIZE A CONTAGEM DA CARGA INTRÍNSECA](../informacao-suporte-design/treino-contagem-carga-intrinseca.md). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.

* [COMO ALBERTO FARIA ESSE CÓDIGO?](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/blob/ad06e72efe9ac775667936a736e3ce633c408d02/src/main/java/com/deveficiente/casadocodigov2/detalhelivro/DetalheLivroSiteController.java) e [aqui](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/blob/ad06e72efe9ac775667936a736e3ce633c408d02/src/main/java/com/deveficiente/casadocodigov2/detalhelivro/DetalheSiteAutorResponse.java)