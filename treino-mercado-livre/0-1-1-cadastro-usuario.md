# Cadastro de novo usuário

## Necessidades

* precisamos saber o instante do cadastro, login e senha.

## Restrições

*   O instante não pode ser nulo e não pode ser no futuro
*   O login não pode ser em branco ou nula
*   O login precisa ter o formato do email
*   A senha não pode ser branca ou nula
*   A senha precisa ter no mínimo 6 caracteres
*   A senha deve ser guardada usando algum algoritmo de hash da sua escolha.

### Resultado esperado

*  O usuário precisa estar criado no sistema
*  O cliente que fez a requisição precisa saber que o usuário foi criado. Apenas um retorno com status 200 está suficente.
* Em caso de falha de validação status 400

### Sobre a utilização do material de suporte aqui

Se você já está no projeto do nosso mercado livre, quer dizer que praticou bastante no projeto da casa do código. A ideia é que você utilize bem menos o material de suporte a partir de agora. Tente sempre fazer baseado nas suas ideias e realmente invista energia para desenrolar a funcionalidade. 

Nesta altura do campeonato deve estar um pouco mais claro a sugestão de divisão de responsabilidade que estamos trabalhando. Você tem uma métrica muito poderosa para focar seu código em fazer funcionar e depois, se precisar, dividir as responsabilidades de um jeito que facilite o entendimento de outras pessoas. 

Caso sinta que precisa de suporte, utilize o material de suporte de maneira bem progressiva. Lembre que também temos nosso canal do discord e você pode pedir uma ajudinha por lá :). 

### **informações de suporte geral**

1.  Será que você fez um código parecido com esse exemplo [aqui](https://drive.google.com/file/d/1TZ57A-QRAmlhyyuqBPW2sTCMr3gtdyP5/view?usp=sharing) ?
2.  Se a resposta para o ponto 1 foi sim, recomendo de novo esse material aqui sobre [arquitetura x design](https://drive.google.com/file/d/1zyoz7tx4iqQI_A6QKRsDG3JvA1f3p1IM/view?usp=sharing). Também acho que vai ser legal você olhar a [minha implementação logo de cara](https://drive.google.com/file/d/1inm4z8yHDh3bnkcbezEshkrb2ILSFq2T/view?usp=sharing), apenas para ter uma ideia de design que estou propondo.
3.  [Controllers 100% coesos](https://drive.google.com/file/d/10f3lT3lB2CEXdyss7ZjeSVzmDkzEU57d/view?usp=sharing) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
4.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://drive.google.com/file/d/1SMwN_Dd9MdWI047o5dGJuBdPygbc6giX/view?usp=sharing)
5.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://drive.google.com/file/d/18Mu6IG0CzuDtTjoPsFJWscOxG2LZvv6O/view?usp=sharing).
6.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://drive.google.com/file/d/1P_860b6FL8mIj9X8yyQyW4B2YNL2kW5V/view?usp=sharing) e depois [aqui](https://drive.google.com/file/d/1BgjdHCbrPP8ZuTRLi5tn2a7iPepr1sCR/view?usp=sharing)
7.  Email e senha são informações obrigatórias. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://drive.google.com/file/d/1988eYtK-AqS6FVET1zO04HzjM6egHoKM/view?usp=sharing)
8.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. Um email por exemplo. Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://drive.google.com/file/d/1TMENbD2V_87FmEGzwjTb4zqUnucsDnKM/view?usp=sharing)?
9.  Ainda sobre as dicas, será que você recebeu a senha do usuário como String no construtor? Se sim, como que o ponto do código que chama aquele construtor sabe que aquela String precisa ser encodada ou não encodada? Você encodou a senha dentro do construtor? E se o outro ponto de código tiver encodado a senha também, vai rolar uma dupla encodada? Como você pode fazer para deixar uma dica ou aumentar a restrição em tempo de compilação?
10.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
11.  [Pegue cada uma das classes que você criou e realize a contagem da carga intrínseca](https://drive.google.com/file/d/1MwuEjVO9evwVsYK5t5hB0q22uHj7CwSQ/view?usp=sharing). Esse é o viés de design que estamos trabalhando. Precisamos nos habituar a fazer isso para que se torne algo automático na nossa vida.
12.  [Como Alberto faria esse código](https://drive.google.com/file/d/1ftB7EmVqRjDyEQRHU3clQJqkiYmBHUJ8/view?usp=sharing)? Parte 2 com o código [resolvendo a questão da senha encodada](https://drive.google.com/file/d/1F44GfX42asAK4EvTcCzkm2epNMnAfprk/view?usp=sharing).

### informações de suporte para a combinação Java/Kotlin + Spring

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://drive.google.com/file/d/1FfYMfcbAODr3RKBFqtj8aj_Ztvjbkfhy/view?usp=sharing)
5.  [Como externalizar as mensagens de erro no arquivo de configuração.](https://drive.google.com/file/d/1FfYMfcbAODr3RKBFqtj8aj_Ztvjbkfhy/view?usp=sharing)