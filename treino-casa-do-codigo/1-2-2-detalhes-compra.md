# Detalhes da compra

## **necessidades**

Agora é preciso retornar todos os dados necessários para que a pessoa visualize os dados da compra dela. Para confirmar que tudo está certinho.

Caso tenha cupom aplicado, além do valor original da compra é necessário mostrar o valor final com o cupom aplicado.

O endpoint recebe apenas o id gerado pela compra.

## **resultado esperado**

*   status 200 e json de detalhes de uma compra
*   Sempre teremos dois campos no json de saída: existeCupom e valorCupom. Caso não tenha cupom, os valores dos campos devem ser false e null respectivamente. 

## **informações de suporte para a feature**

1.  Controllers 100% coesos
2.  Separamos as bordas externas do sistema do seu núcleo. Não ligamos parâmetros de requisição externa com objetos de domínio diretamente, assim como não serializamos objetos de domínio para respostas de API.
3.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint