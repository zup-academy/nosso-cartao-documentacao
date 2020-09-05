# Exibir lista de livros

## Contexto

Aqui é uma atividade para que você trabalhe o retorno de dados da api e também para que você tenha uma forma fácil de ver os ids dos livros criados.

## necessidades

* Para que seja fácil pegar um id do livro, vamos exibir a lista de livros cadastrados. 

## resultado esperado

* Em caso de sucesso retorne 200 e no corpo da resposta envie o json com a lista de livros
* Em caso de problemas, retorne 500.

## informações de suporte

* [CONTROLLERS 100% COESOS](../informacao-suporte-design/controllers-100-coesos.md) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.

* [Separamos as bordas externas do sistema do seu núcleo. Não ligamos parâmetros de requisição externa com objetos de domínio diretamente, assim como não serializamos objetos de domínio para respostas de API.](../informacao-suporte-design/nao-serializamos-objetos-de-dominio-para-respostas-de-api.md)

* Utilize um insomnia ou qualquer outra forma para verificar o endpoint

* [PEGUE CADA UMA DAS CLASSES QUE VOCÊ CRIOU E REALIZE A CONTAGEM DA CARGA INTRÍNSECA](../informacao-suporte-design/treino-contagem-carga-intrinseca.md). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.

* [COMO ALBERTO FARIA ESSE CÓDIGO?](https://github.com/asouza/jornada-deveficiente-casa-do-codigo/commit/eb6f3fec10d2801a076127cf74b2ec81cf54aeb2)