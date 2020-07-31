# Segurança de aplicações cloud-native

Aplicações com características cloud-native estão aptas a rodar em múltiplos ambientes, isso
faz com que não tenhamos certeza de quais níveis de segurança estão aplicados em determinados 
ambientes. Por esse motivo devemos nos preocupar com ainda mais segurança nesse contexto.

Provedores de nuvem pública possuem um elevado nível de segurança, mas pouco adianta se nossas
aplicações não implementarem e seguirem boas práticas de segurança.







## Incorpore segurança no design

Segurança deve ser tratada igualmente como qualquer outra feature do seu sistema. Durante
todo o processo de desenvolvimento preocupações inerentes a segurança devem ser levantadas e
tratadas de maneira regular e com frequência. 

Incorporar segurança no seu design é um princípio bastante importante.


## Rode sua aplicação com o mínimo de privilégios

Provavelmente sua aplicação deve se conectar ou utilizar serviços adicionais para o funcionamento.

Garanta que sua aplicação utilize somente o conjunto de permissões que ela necessita. Exemplo
se sua aplicação precise de acesso de leitura no banco de dados crie uma conta que permita somente leitura,
não conceda privilégio de escrita sem a necessidade. Esse tópico garante que nossa aplicação
reduza o espaço ou brechas de segurança.



# Informação de Suporte




## Dicas Claudio
- Sempre consulte a equipe de segurança nos momentos de dúvidas, essa equipe é destacada
para garantir que todos nossos sistemas sejam seguros e sigam a regra de compliance da Zup.