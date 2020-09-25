# Você precisa entender o que está usando e olhar sempre o lado negativo de cada decisão.

Por mais clichê que isso seja, continua sendo verdade. Quase tudo na vida tem lado positivo e negativo. E aí você busca sempre tomar decisões que tenham mais coisas positivas do que negativas. É até óbvio, convenhamos. 

Quando pensamos em desenvolvimento de software, tomamos várias decisões das mais variadas escalas. É mais do que necessário sermos capazes de analisar sempre que o estamos deixando na mesa para cada uma delas. Vamos tentar pegar alguns cenários. 

## Decidi adotar CDD como linha de design de código

A teoria proposta pelo CDD(Cognitive Driven Development) diz que você deve buscar dividir as responsabilidades do código pela linha do entendimento humano. Ela parece promissora e tudo mais, mas existem alguns pontos de atenção:

* Quantos projetos já foram desenvolvidos apoiados nela?
* Será que quando o sistema ficar maior, vamos mesmo conseguir controlar a crescente de complexidade por unidade?
* Dependendo da métrica, podemos ter muitas unidades de código gerada. Será que isso realmente vai facilitar?

## Decidi utilizar uma inspiração arquitetural com muitas camadas

Como já falamos, um software pode ser escrito de diversas maneiras diferentes. Existem estratégias arquiteturais que buscam facilitar a troca de componentes do software que não são intimamente conectadas com o código que resolve o negócio em si. Algumas possíveis peças que você pode querer trocar:

* Framework web;
* Framework de acesso a banco de dados;
* Biblioteca que realiza requisições externas;
* Protocolo utilizado para entregar os dados de entrada da aplicação;
* Execução síncrona para assíncrona;

Você pode preparar seu código para qualquer uma das possíveis mudanças listadas acima. Será que conseguimos olhar alguns pontos de atenção?

* Toda indireção aumenta complexidade, como vou lidar com isso?
* E se eu nunca quiser trocar tais componentes?
* Será que viver sob esse conjunto de abstração não vai deixar minha produção de código mais lenta?

## Decidi utilizar uma arquitetura distribuída

Vamos supor que sua equipe pretende criar ou evoluir um software agora apostando numa arquitetura distribuída, pouco importa qual. Quais são os possíveis pontos de atenção, será que conseguimos listar alguns?

* Como vou lidar com o fato de uma operação agora acontecer sequencialmente em vários sistemas diferentes?
* Vou me preocupar com conceitos de transação distribuída, preciso?
* Como vou lidar com a lentidão que pode acontecer em algum ponto da comunicação?
* Será que o ganho de flexibilidade que vou ter, supera a provável perda de performance por conta da comunicação distribuída?
* Como vou lidar com os contratos de borda? 

## Conseguir olhar para os pontos de atenção é uma restrição

Se você não for capaz de olhar para os pontos de atenção/negativos, talvez você não deva optar por aquele caminho naquele momento. Caso opte, é importante ter na mente que você está indo por um caminho que não sabe dos perigos e isso pode afetar sua visão de futuro, antecipação etc. 

## Quantos pontos de atenção eu devo levantar?

Pense aqui como se fosse uma análise de causa raiz. Quanto mais pontos de atenção, melhor. Quer dizer que você realmente tem uma visão crítica sobre aquela decisão e parece estar preparado(a) para lidar com um leque maior de situações que podem aparecer no futuro. 
