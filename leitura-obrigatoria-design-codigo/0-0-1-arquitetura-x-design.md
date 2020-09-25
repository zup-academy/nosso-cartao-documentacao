# Arquitetura x Design

​Muito se fala sobre arquitetura x design de código. Não parece interessante levar horas falando sobre isso, então podemos resumir da seguinte forma: arquitetura é transversal para todo o sistema e para múltiplos sistemas diferentes enquanto que o design de código, até hoje, sempre foi específico. 

Durante muito tempo focamos muito na arquitetura, nos seus mais variados níveis:

* Qual é a infraestrutura que vamos utilizar aqui? Vai ser cloud native?
* Qual estilo de separação de camadas vamos usar aqui? Hexagonal, Clean arch, Onion etc? Percebe que MVC ficou tão padrão, que nem falamos mais. 
* Como vamos lidar com a questão da segurança dos dados?

Todas essas preocupações são muito importantes, mas insuficientes. Falta um pedaço chave aí: o código específico que vai ser produzido. Cansamos de ver classes gigantes, com uma estratégia ineficiente de separação de interesses/responsabilidades dentro do chamado domínio da aplicação. Pouca importa o estilo arquitetural que você escolheu no tocante ao código em si, em algum lugar dele vai existir classes relativas ao problema real que está sendo resolvido. 

**Precisamos de uma arquitetura para nosso design :)**. Os livros e práticas que foram escritos até hoje não foram suficientes. E olha que já tivemos centenas, talvez milhares, de livros publicados sobre divisão de responsabilidades e organização de um código. 

É necessároi buscar um linha mestra relativa ao design e que possa ser aplicável para a maioria dos sistemas que você for implementar. Como maximizar a chance que sistemas pequenos, médios e grandes sejam divididos de modo que a maioria das pessoas possa entender? Como tentar garantir essa régua mesmo quando você estiver na maior pressão da sua vida? 

Vamos buscar por um design de código que seja sustentável no médio e longo prazo e também escalável quando pensamos em tamanhos de equipe.