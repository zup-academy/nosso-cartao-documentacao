# Quando devo encriptar dados no meu banco de dados???

Nossa aplicação geralmente manipula alguns tipos de dados, algumas vezes dados relacionados a transações financeiras, 
outras vezes relacionados a dados de produtos. 

Mas e quando lidamos com dados de pessoas **físicas** ou **jurídicas**?? Como vamos guardar algumas informações que permitam
identificar uma pessoa no banco de dados??

Alguns projetos devem manipular de uma maneira especial essas informações, elas devem ser armazenadas de maneira "embaralhada"
ou criptografada tecnicamente, isso adiciona uma "camada" extra de segurança nos nossos dados.

Perceba que se alguém não autorizado tiver acesso a informação, nada vai adiantar porque os dados estão "embaralhados" de maneira
que a informação original seja preservada.

**Observação**: Esteja bastante atento aos requisitos de segurança das suas informações, cada projeto tem seu nível de criticidade e **sempre** pergunte
caso você tenha alguma dúvida sobre segurança, na Zup temos um time que pode te ajudar!!!

Os dois modelos de criptografia são **Assimétricos** onde a informação é encriptada com uma chave de criptografia e "descriptografada" com outra
chave diferente da chave de criptografia.

O outro modelo é mais simples, chamade de **Simétrico** onde a mesma chave é utilizada para "criptografar" e "descriptografar". 

Cada um desses modelos tem seus prós e contras e pode ser utilizado de acordo com a necessidade do seu projeto!!!

E ae no nosso projeto de cartão, precisamos armazenar algum dado criptografado??? Em algum lugar utilizamos dados que identificam
uma pessoa???

Uma parte bastante importante neste item é que existem diversas formas de realizar a criptografia dos dados no processo de armazenamento.
Podemos fazer isso na nossa aplicação, de maneira que antes de persistir realizamos o processo de criptografia.

Ou em alguns casos, quando aplicado, alguns provedores de nuvem oferecem serviços de maneira que os dados antes de serem persistidos
no banco de dados por exemplo seja criptografado na própria infraestrtura do provedor, eliminando a necessidade de "tratarmos" a criptografia.

**Observação**: Não há um modelo mais adequado, isso é uma decisão de projeto que pode levar em consideração caso de uso e
requisitos de segurança.


# Informação de Suporte
* Se por algum motivo você se interessou pelo assunto de criptografia, [esse link define uma série de termos bem importantes
nesse contexto](https://www.ssl2buy.com/wiki/symmetric-vs-asymmetric-encryption-what-are-differences)
* [Este link](https://searchsecurity.techtarget.com/definition/asymmetric-cryptography) pode te ajudar entender criptografia assimétrica
* Se você quiser se aprofundar no modelo de criptografia simétrico, [este link pode te ajudar](https://www.cryptomathic.com/news-events/blog/symmetric-key-encryption-why-where-and-how-its-used-in-banking)