# Sugestão de como realizar testes dentro da Jornada

[Neste vídeo](https://youtu.be/R5qhgEqrhFw) falamos sobre a sugestão de approach para criarmos os testes automatizados dentro da jornada. 

Vamos combinar fortemente boundary testing, structural testing através de uma visão diferente do MC/DC e também vamos olhar muito para self testing. 

Enquanto que o self testing em si não está diretamente ligado ao fato de escrevermos testes automatizados, as outras estão. E aqui um ponto importante: tais técnicas não tem ligação direta com testes de unidade! Você pode pensar em cobertura e testar valores limite para qualquer tipo de teste que vá escrever, seja ele de unidade, integrado, de sistema ou manual. 

Para a jornada em si, vamos focar demais em testes de unidade. A ideia vai ser elevar a régua dos nossos testes de unidade automatizados, buscando escrever cada um de maneira sistemática. Ou seja, isso precisa ser escalável para a equipe toda. Dado um método, todas as pessoas da equipe precisam escrever um conjunto de testes muito parecido, muitas vezes até igual. 

Em relação a cobertura, a sugestão é focar na MC/DC, mas diferente do que o livro de Aniche sugere. Enquanto que pela literatura formal, a MC/DC engloba a cobertura por linhas básicas, aqui na Jornada vamos focar literalmente em só cobrir  com testes métodos que tenham branches escritas. Ou seja, um método que tem apenas um fluxo, por esse olhar, pode ser negligenciado. A não ser que ele seja tocado por um teste de unidade em cima de uma branch. 

A tática de cobertura acima é perigosa? Talvez sim. Por outro lado, não adianta cobrir um monte de linha com testes de unidade enquanto que as "principais" linhas não estão tão bem cobertas. No final das contas, de tanto fazer teste para cobrir branch, você vai estar confortável para sair do outro lado com outros estilos de cobertura. 

Por fim, não vamos dar tanta ênfase no testes gerados a partir de especificações. Se quiser, tente explorar o tópico quando tiver analisando as especificações de funcionalidades aqui da jornada. 
