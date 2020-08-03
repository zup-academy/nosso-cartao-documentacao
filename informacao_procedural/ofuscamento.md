# O que é ofuscamento ??? Quando devo usá-lo ???

Nos desenvolvedores usamos os logs da nossa aplicação como uma ferramenta de encontrar
problemas, normalmente nossos logs indicam os passos ou informações que nos ajudam a direcionar
a resolução desses problemas. Se você tem dúvidar de como usar de maneira eficiente, [aqui você pode encontrar alguns direcionamentos]().

Em alguns casos precisamos "logar" algumas informações que possam identificar uma pessoa e nesse caso
que começam nossos problemas. 

Sempre que você precisar "logar" uma informação que seja passível de identificação
de uma pessoa é necessário realizar o ofuscamento do dado. O ofuscamento é uma prática que "embaralha"
os caracteres para proteger nossa informação de maneira que se a informação for analisada por qualquer fonte
não seja possível identificar o dado. O termo adequado para dados que permitam idenficar uma pessoa é 
PII _Personal Identifiable Information_

## Mas quais são os dados que eu devo tomar cuidado ao logá-los ???
A regra geral é sempre que tiver dúvida pergunte ao time de segurança da ZUP *(link aqui)*. 
Em geral documentos pessoais, número de cartões de credito, senhas, informações pertinentes a saúde e informações que dizem aos dados pessoais devem ser 
ofuscadas no log da nossa aplicação ou qualquer outra camada que haja escrita do dado. 

### Exemplos de ofuscação

| Informação          | Aberta            | Ofuscada         |
| -------------       | -------------     | -------------    |
| **Cartão Crédito**  | 4716750056121368  | ************1368 |
| **CPF**             | 635.247.373-31    | 635.***.***-31   |
| **Email**           | joe@doe.com       | j**@***.com      |

Perceba que com essas informações não é possível realizar a identificação da pessoa pelo
documento ou email, o mesmo vale para o cartão de crédito não é possível utilizá-lo em qualquer
compra.

## Mas qual lugar ou camada eu preciso ofuscar dados???

Você deve ofuscar dados sensíveis sempre, sempre que houver um log com dado sensível. Os lugares mais
comuns são:
- Logs de aplicação
- Logs de APIs no API Manager 

## Informações de Suporte

Tem alguma dúvida sobre o que é PII. Neste [link](https://www.gsa.gov/reference/gsa-privacy-program/rules-and-policies-protecting-pii-privacy-act) tem uma breve descrição do termo.

O produto API Manager da Zup suporta ofuscação na camada de APIs, se você quer saber como podemos isso, [Clique Aqui](link manager aqui)


