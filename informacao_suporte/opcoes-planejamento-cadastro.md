## Um planejamento de cadastro padrão do mercado

1. Crio controller
2. Recebo os dados
3. Mando os dados para um service/usecase
4. Converto os dados para um objeto de domínio utilizando alguma classe de conversão
5. Chamdo um repository para salvar
6. Retorno o objeto do service/usecase para o controller
7. Gero a resposta para o cliente

Este é um fluxo muito comum no mercado. As camadas são estabelecidas, independente da necessidade real delas. Se você planejou assim, [eu já te convido a ver a versão que implementamos aqui.](https://github.com/albertotavareszup/nosso-cartao-v2/blob/cria-proposta/src/main/java/br/com/zup/nossocartao/novaproposta/CriaNovaPropostaController.java) Talvez seja um choque de realidade, mas também vai servir para dar outra perspectiva. 