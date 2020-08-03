# E meus usuários ficam aonde ficam...Devo criar um sistema para controlar as permissões dele???

Quando vamos desenvolver uma aplicação sempre precisamos de um controle de usuários. Essas aplicações
buscam algum método de autenticação ou para casos mais avançados controles de autorização.

Nosso primeiro passo aqui é conseguir desacoplar os mecanismos de autenticação e autorização que 
são utilizados para fins diferentes.

Tem dúvida sobre qual a diferença sobre autenticação e autorização??? [Esse link pode ter ajudar](autenticacao_vs_autorizacao.md)

Criar um sistema com essas características é uma tarefa bastante difícil. Deveríamos nos preocupar
em manter a armazenar dados com segurança, construir algoritmos que estejam aptos a armazenar essas informações
de maneira segura e garantir e conseguir trabalhar de maneira eficiente na geração de tokens.
Também devemos estar aptos a criar mecanismos que garantam a estabilidade e confiabilidade
da aplicação em situações de alta volumetria.

Devido a todas estas complexidades existe uma categoria de sistemas que se preocupam com todos esses
requisitos e ainda são experts em segurança. Por isso uma boa prática quando 
vamos criar uma aplicação é considerar _delegar_ esse controle para um sistema
externo à nossa aplicação de maneira que nossa aplicação apenas "consuma" os dados gerenciados por estes
sistemas.

Essa categoria é chamada de IAM _Identity Access Management_, eles nos provêem uma maneira
bastante simplificada para manter esses controles de usuário.


## Dicas Claudio
- Sempre utilize um IAM para manter o controle de seus usuários, esse tipo de solução garante uma estabilidade
e alto nível de segurança para nossas aplicações 

## Informações de Suporte

- Tem dúvida do que é um IAM, este [link pode te ajudar!!!](https://www.cloudflare.com/learning/access-management/what-is-identity-and-access-management/)
- Quer uma visão bastante simplificada do que um IAM deve fazer. [Aqui você encontra](https://www.gartner.com/en/information-technology/glossary/identity-and-access-management-iam)
 