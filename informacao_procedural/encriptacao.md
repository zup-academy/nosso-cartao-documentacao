# Quando devo encriptar dados em trânsito??? Mas para que isso serve ???

Nossas aplicações nunca vivem sozinhas, sempre precisamos realizar chamadas para outras aplicações para
concluir uma determinada tarefa, ou mesmo para persistir nossas informações no banco de dados.

Essas aplicações se comunicam via rede, ou seja há uma transmissão de dados entre as aplicações.
Imagine o seguinte contexto, algum agente mal-intencionado consegue interceptar a comunicação e "roubar"
os dados que estão passando por esse canal. Não parece ser víavel estar sujeito esse tipo de situação.

Vamos ver um exemplo:

![alt text](../images/non-tls.png "comunicacao_nao_segura")


Para nos proteger desses ataques **sempre** precisamos usar um canal de comunicação seguro, um modelo
que nos permita nos autenticar e realizar a encriptação da mensagem antes do envio. Neste caso quando o 
atacante obter acesso as informações essas informações vão estar criptogradas de maneira que a informação
não tenha serventia ao atacante.

Vamos ver um exemplo:

![alt text](../images/tls.png "comunicacao_segura")

Perceba que o canal de transmissão está protegido, o acesso a informação fica muito
mais complexo para o atacante, isso exige muito mais esforço e minimiza consideravelmente
as chances de termos informações expostas. 

#Como encriptar dados em trânsito ???




# Informações de Suporte





