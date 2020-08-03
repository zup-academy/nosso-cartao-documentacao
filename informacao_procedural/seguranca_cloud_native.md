# Segurança de aplicações cloud-native

Aplicações com características cloud-native estão aptas a rodar em múltiplos ambientes, isso
faz com que não tenhamos certeza de quais níveis de segurança estão aplicados em determinados 
ambientes. Por esse motivo devemos nos preocupar com ainda mais segurança nesse contexto.

Provedores de nuvem pública possuem um elevado nível de segurança, mas pouco adianta se nossas
aplicações não implementarem e seguirem boas práticas de segurança.

O processo de adição de segurança deve ser iniciado no momento da criação
do projeto e continuamente sendo trabalhado junto com cada nova feature. Mas você deve
estar pensando em como fazer isso. Como criar esse mindset de segurança, está com
essa dúvida??? [clique aqui](incorpore_seguranca_design.md)

Pronto, durante o processo de desenvolvimento entendi que preciso tomar cuidado
com as novas features e verificar se elas causam algum problema de segurança.

Tem mais alguma coisa que eu possa fazer durante a fase de desenvolvimento para minimizar
minhas chances de ser atacado ou que meus dados sejam comprometidos??? Existem técnicas
que nos ajudam com isso, quer saber delas [clique aqui!!!](ofuscamento.md) 
 



Mas e na fase de produção, quando sistema já esta sendo executado pelo usuário
final. Tem alguma técnica que eu possa aplicar para reduzir ainda mais os riscos??






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