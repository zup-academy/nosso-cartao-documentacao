# Começo do fluxo de pagamento

## necessidades
Uma coisa importante. Na cdc, você não faz um cadastro e tem suas compras associadas. Toda vez você coloca seu email, cpf etc. Como isso vai ser implementado depende da aplicação.

Os seguintes campos precisam ser preenchidos:

* email
* nome
* sobrenome
* documento(cpf/cnpj)
* endereco
* complemento
* cidade
* país
* estado(caso aquele pais tenha estado)
* telefone
* cep

### restrição

* email obrigatório e com formato adequado
* nome obrigatório
* sobrenome obrigatório
* documento(cpf/cnpj) obrigatório e só precisa ser um cpf ou cnpj
* endereco obrigatório
* complemento obrigatório
* cidade obrigatório
* país obrigatório
* estado (apenas se o país tiver cadastro de estados)
* telefone obrigatório
* cep é obrigatório

### resultado esperado

* Aqui ainda estamos no meio do processo. Então no final desta etapa você precisa ter um endpoint criado recebendo os dados da pessoa que está comprando e com os dados validados. Retorne 200 em caso de sucesso.
* Em caso de falha de validação retorne status 400
