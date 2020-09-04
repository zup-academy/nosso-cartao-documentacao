# Criar um novo livro

## necessidades

* Um título
* Um resumo do que vai ser encontrado no livro
* Um sumário de tamanho livre. O texto deve entrar no formato markdown, que é uma string. Dessa forma ele pode ser formatado depois da maneira apropriada.
* Preço do livro
* Número de páginas
* Isbn(identificador do livro)
* Data que ele deve entrar no ar(de publicação)
* Um livro pertence a uma categoria
* Um livro é de um autor

## restrições

* Título é obrigatório
* Título é único
* Resumo é obrigatório e tem no máximo 500 caracteres
* Sumário é de tamanho livre. 
* Preço é obrigatório e o mínimo é de 20
* Número de páginas é obrigatória e o mínimo é de 100
* Isb é obrigatório, formato livre
* Isbn é único
* Data que vai entrar no ar precisa ser no futuro
* O id da categoria é obrigatório
* O id da categoria precisa existir no banco de dados
* O id do autor é obrigatório
* O id do autor precisa existir no banco de dados

## resultado esperado
* Em caso de sucesso retorne 200
* Em caso de falha de validação retorne 400

