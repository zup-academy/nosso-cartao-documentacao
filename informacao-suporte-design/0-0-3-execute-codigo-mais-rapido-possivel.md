# Execute o seu código o mais rápido possível

A prioridade básica de um software é funcionar e já falamos sobre isso no pilar "A prioridade máxima é funcionar de acordo com o caso de uso. Beleza e formosura não dão pão nem fartura". E como você pode abraçar essa ideia de fato enquanto desenvole?

## Comece pela entrada de dados do caso de uso

Para cada funcionalidade necessária de ser implementada vai existir uma forma de entrada de dados. Aqui temos alguns exemplos:

* Via requisição HTTP;
* Via mensageria;
* Via processamento em batch;

A sugestão é que você comece seu código por aí. Dessa forma você vai ter a chance de executar o seu código o mais rápido possível e mais vezes durante a implementação. 

## Exemplo de fluxo começando pela entrada de dados

Suponha que você está implementando uma api que recebe dados via HTTP para suportar o funcionamento de criação de propostas para cartões crédito. Um fluxo de implementação que começa pela entrada de dados seria o seguinte:

* Já vai no Insomnia, Postman, curl ou qualquer cliente e mapeia a requisição que você quer;
    * Aqui, de maneira até ingênua, já podemos executar! Mesmo sabendo que vai dar 404;

* Cria agora o método que vai ser mapeiado para receber os dados da requisição;
    * aqui você já pode executar para verificar se a requsição está chegando;

* Cria a classe ou a abstração específica na linguagem escolhida para receber os dados que estão vindo na requisição;
    * já pode executar de novo para verificar se os dados estão chegando;

* Trabalha em cima das validações necessárias para proteger a borda do sistema;
    * mais uma chance de executar;

* Converte o objeto que representa a requisição com os dados da proposta para seu objeto de domínio que realmente tem os atributos que representam os dados necessários do sistema e que vão ser persistidos;
    * mais uma chance de executar o código e verificar se tudo está indo como deveria;

* Salva o objeto no banco de dados;
    * executa de novo;

* Manda uma mensagem para o sistema externo que precisa ser avisado da proposta;
    * executa de novo;   

Perceba que no mínimo você executou seu código sete vezes antes de completar a implementação. E tudo isso em cima do fluxo real, ou seja, quando você acabar realmente vai estar com a implementação pronta. 

## Cada execução é uma chance de pegar um possível bug mais cedo

Cada vez que você executa você tem a chance de pegar o bug mais cedo e isso é muito positivo. **Quanto mais tempo você demora para executar o seu código, maior é a chance de ter um bug ali que você não está percebendo**. 

Agora você pode criar seus testes automatizados para que eles tentem revelar ainda mais bugs :). 

