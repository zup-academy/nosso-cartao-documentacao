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