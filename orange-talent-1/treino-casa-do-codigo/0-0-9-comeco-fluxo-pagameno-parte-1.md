# Começo do fluxo de pagamento

### **necessidades**

Uma coisa importante. Na cdc, você não faz um cadastro e tem suas compras associadas. Toda vez você coloca seu email, cpf/cnpj etc. Como isso vai ser implementado depende da aplicação.

Os seguintes campos precisam ser preenchidos:

*   email
*   nome
*   sobrenome
*   documento(cpf/cnpj)
*   endereco
*   complemento
*   cidade
*   pais
*   estado(caso aquele pais tenha estado)
*   telefone
*   cep

### **restrição**

*   email obrigatório e com formato adequado
*   nome obrigatório
*   sobrenome obrigatório
*   documento(cpf/cnpj) obrigatório e só precisa ser um cpf ou cnpj
*   endereco obrigatório
*   complemento obrigatório
*   cidade obrigatório
*   país obrigatório
*   se o país tiver estados, um estado precisa ser selecionado
*   estado(caso aquele pais tenha estado) - apenas se o país tiver cadastro de estados
*   telefone obrigatório
*   cep é obrigatório

### **resultado esperado**

*   Compra parcialmente gerada, mas ainda não gravada no banco de dados. Falta os dados do pedido em si que vão ser trabalhados no próximo cartão.

### **sobre a utilização do material de suporte aqui**

Este começo de fechamento de compra envolve muitos passos. Decidimos começar pegando apenas os dados do formulário relativo a pessoa que está comprando. Este é um formulário um pouco mais desafiador, já que possuímos algumas validações customizadas que precisam ser feitas. Não tem nada que você não tenha trabalhado até aqui, mas é mais uma chance de você treinar sua habilidade para conhecer mais das tecnologias e colocar em prática alguns dos pilares que vem nos norteando. ​

### **informações de suporte para a feature**

1.  [A prioridade do código é funcionar](https://youtu.be/K1U1vzlPaVU). Se você tentar implementar tudo necessário para criar a versão inicial da compra, vai demorar muito para ver seu código rodando a primeira vez. Lembre que quanto mais você demora de rodar, maior é a chance de ter mais de um problema na primeira execução. [Olhe também este outro vídeo sobre a importância de priorizar o funcionamento do código](https://youtu.be/-WUFmUeeFro)
2.  [Controllers 100% coesos](https://youtu.be/NNKG2TFctfo) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
3.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://youtu.be/AzyHKZwNg1A)
4.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://youtu.be/kzjSxBDQXp8). Esse aqui é um formulário bem mais complexo, pois provavelmente vai possuir muito mais dependências. Vai ser um belo desafio.
5.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://youtu.be/XPXOhvrJT1w) e depois [aqui](https://youtu.be/kkKqo80whqo)
6.  [Favorecemos a coesão através do encapsulamento](https://youtu.be/HGcQlsynTuM). Como você planeja validar se o documento é válido?
7.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
9.  [Como Alberto faria esse código?](https://youtu.be/Oba10gpoyKQ)
