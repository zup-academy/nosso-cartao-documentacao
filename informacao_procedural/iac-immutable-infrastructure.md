# Entendendo um pouco de Infrastructure as Code e Immutable Infrastructure!!!

Uma maneira bastante interessante de lidar com a configuração das nossas aplicação é um padrão chamado
_Infrastructure as a Code_, a idéia desse princípio é bastante simples, você deveria ser capaz de criar
sua infra estrutura a partir de um código fonte versionado em algum repositório de código.
A parte legal desse princípio é que normalmente já fazemos isso com nossas aplicações, armazenamos nosso código
fonte em um git por exemplo, então é relativamente tranquilo fazer o mapeamento mental.

Quando aplicamos conceito de IaC **(_Infrastructure as a Code_)** automaticamente já aplicamos uma prática bastante recomendada quando pensamos
em ambiente de nuvem, a prática chamada _Immutable Infrastructure_ **(infra-estrutura imutável)**, indica que uma vez que criamos
um elemento de infra-estrurura não podemos modificá-lo.

Quando precisamos alterar nosso elemento de infra-estrtura, devemos destrui-lo, alterar a receita e criá-lo novamente. Isso nos traz um benefício bastante
interessante que é a capacidade de replicar o ambiente quando quisermos. Muito massa isso né?? Uma simples prática
que nos ajuda muito!!! 

# Informações de suporte

* Se em algum momento você pode ter pensado "Quero aprender mais sobre Infrastructure as a Code"
  * [Aqui você encontra uma explicação](https://www.hashicorp.com/resources/what-is-infrastructure-as-code/) um pouco mais histórica da necessidade de versionarmos nosso código fonte
  * Se ainda você quer se aprofundar ainda mais [esse link vai resolver muitas dúvidas](https://www.ibm.com/cloud/learn/infrastructure-as-code)
* Talvez você queira mais detalhes sobre o que é Immutable Infrastrucure?? [Aqui tem uma definição bem interessante!!!](https://www.hashicorp.com/resources/what-is-mutable-vs-immutable-infrastructure/)
* Ou ainda pode estar se perguntando "Esse negócio é novo???" [aqui tem um link bem legal que explica detalhes](https://www.oreilly.com/radar/an-introduction-to-immutable-infrastructure/),
 repare na data 9 de Junho de 2015!!!Opss não é tão novo assim!!!


  



