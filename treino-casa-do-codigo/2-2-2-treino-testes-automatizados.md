# Treino de testes automatizados

**Antes de continuar essa atividade, é necessário que você pare e consuma mais um conteúdo teórico**. Criamos um material adicional para que você possa entrar ainda mais de cabeça no mundo dos testes automatizados. Você deve assistir todos os vídeos que estão [aqui](../testes-automatizados-reveladores-de-bugs). É um material denso, mas que vai te dar muita teoria interessante sobre como escrever testes automatizados de maneira sistemática e que realmente aumente a confiabilidade de execuçao do seu sistema.

Dada a sugestão de escrever os testes depois de implementar as funcionalidades, também foi sugerido uma adaptação da técnica de cobertura MC/DC para decidir quais pontos do código seriam testados. A ideia é pegar apenas os pontos do código onde temos condicionais e/ou branches.

Dessa forma concentramos energias nos pontos mais críticos do código e tentamos escrever os melhores testes que conseguimos. A contrapartida é que a nossa cobertura de linhas cai. No final, o saldo ainda tende a ser positivo, pois se você consegue cobrir os pontos mais críticos não tem porque não se adaptar a um ambiente onde seja necessário cobrir linhas mais fáceis.

No código desenvolvido por Alberto, tivemos os seguintes testes automatizados criados:

1.  Testes relativos a classe **NovoLivroRequest**. [Confira aqui](https://drive.google.com/file/d/1owVMSScq7xb6MKbt9oFJ4mysHBLR5XZ8/view?usp=sharing).
2.  Testes relativos a classe **Cupom**. [Confira aqui](https://drive.google.com/file/d/1DBHP_-ZwMi_g6PaHuEqcnZ0obTiMfUyG/view?usp=sharing).
3.  Testes relativos a classe **NovaCompraRequest**. [Confira aqui](https://drive.google.com/file/d/1ksCNelWVO-6hvw2oyhldVzDo64juHSCg/view?usp=sharing)
4.  Testes relativos a classe **Pedido**. [Confira aqui](https://drive.google.com/file/d/1dMnd5woygfSgw8agTkdoIDhS_jE0Y1Sb/view?usp=sharing)