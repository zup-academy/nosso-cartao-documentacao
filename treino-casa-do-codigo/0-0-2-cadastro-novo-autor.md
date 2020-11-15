# Cadastro novo autor

### **necessidades**

*   É necessário cadastrar um novo autor no sistema. Todo autor tem um nome, email e uma descrição. Também queremos saber o instante exato que ele foi registrado.

### **restrições**

*   O instante não pode ser nulo
*   O email é obrigatório
*   O email tem que ter formato válido
*   O nome é obrigatório
*   A descrição é obrigatória e não pode passar de 400 caracteres

### **resultado esperado**

*   Um novo autor criado e status 200 retornado

### **informações de suporte geral**

1.  Será que você fez um código parecido com esse exemplo [aqui](https://drive.google.com/file/d/1TZ57A-QRAmlhyyuqBPW2sTCMr3gtdyP5/view?usp=sharing) ?
2.  Se a resposta para o ponto 1 foi sim, recomendo de novo esse material aqui sobre [arquitetura x design](https://drive.google.com/file/d/1zyoz7tx4iqQI_A6QKRsDG3JvA1f3p1IM/view?usp=sharing). Também acho que vai ser legal você olhar a [minha implementação logo de cara](https://drive.google.com/file/d/1inm4z8yHDh3bnkcbezEshkrb2ILSFq2T/view?usp=sharing), apenas para ter uma ideia de design que estou propondo.
3.  [Controllers 100% coesos](https://drive.google.com/file/d/10f3lT3lB2CEXdyss7ZjeSVzmDkzEU57d/view?usp=sharing) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
4.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://drive.google.com/file/d/1SMwN_Dd9MdWI047o5dGJuBdPygbc6giX/view?usp=sharing)
5.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://drive.google.com/file/d/18Mu6IG0CzuDtTjoPsFJWscOxG2LZvv6O/view?usp=sharing).
6.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://drive.google.com/file/d/1P_860b6FL8mIj9X8yyQyW4B2YNL2kW5V/view?usp=sharing) e depois [aqui](https://drive.google.com/file/d/1BgjdHCbrPP8ZuTRLi5tn2a7iPepr1sCR/view?usp=sharing)
7.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://drive.google.com/file/d/1wc5ChsPeGFjqypb9QI7tGRMl9dn0WkkL/view?usp=sharing)
8.  Nome,email e descrição são informações obrigatórias. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://drive.google.com/file/d/1988eYtK-AqS6FVET1zO04HzjM6egHoKM/view?usp=sharing)
9.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. Um email por exemplo. Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://drive.google.com/file/d/1TMENbD2V_87FmEGzwjTb4zqUnucsDnKM/view?usp=sharing)?
10.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
12.  [Como Alberto faria esse código](https://drive.google.com/file/d/1inm4z8yHDh3bnkcbezEshkrb2ILSFq2T/view?usp=sharing)?

### **informações de suporte sobre o Spring e JPA**

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://drive.google.com/file/d/18q7IUF1EmeGrPFAab1CHIXP3COf5KNHd/view?usp=sharing)
5.  [Como externalizar as mensagens de erro no arquivo de configuração.](https://drive.google.com/file/d/1FfYMfcbAODr3RKBFqtj8aj_Ztvjbkfhy/view?usp=sharing)

