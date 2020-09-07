# Detalhes da compra

## necessidades
Agora é preciso retornar todos os dados necessários para que a pessoa visualize os dados da compra dela. Para confirmar que tudo está certinho. 

Caso tenha cupom aplicado, além do valor original da compra é necessário mostrar o valor final com o cupom aplicado. 

## resultado esperado

* status 200 e json de detalhes de uma compra

## informações de suporte

* [CONTROLLERS 100% COESOS](../informacao-suporte-design/controllers-100-coesos.md) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.

* Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [DÁ UMA OLHADA NESSE PILAR AQUI](../informacao_suporte/recebe-dados-requisicao.md).

* Utilize um insomnia ou qualquer outra forma para verificar o endpoint

* [PEGUE CADA UMA DAS CLASSES QUE VOCÊ CRIOU E REALIZE A CONTAGEM DA CARGA INTRÍNSECA](../informacao-suporte-design/treino-contagem-carga-intrinseca.md). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.