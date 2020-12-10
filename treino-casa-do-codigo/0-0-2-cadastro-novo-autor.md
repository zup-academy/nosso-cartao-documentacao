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

1.  Será que você fez um código parecido com esse exemplo [aqui](https://youtu.be/hSab_VHL98Q) ?
2.  Se a resposta para o ponto 1 foi sim, recomendo de novo esse material aqui sobre [arquitetura x design](https://youtu.be/BaLEcX_Bh1k). Também acho que vai ser legal você olhar a [minha implementação logo de cara](https://youtu.be/CghDgad4jWI), apenas para ter uma ideia de design que estou propondo.
3.  [Controllers 100% coesos](https://youtu.be/i3Au8Slv3x4) para lembrar você a nossa ideia de ter controllers que utilizam todos os atributos.
4.  Como foi que você fez para receber os dados da requisição? Será que aproveitou a facilidade do framework e recebeu a sua entidade(objeto que faz parte do domínio) direto no método mapeado para um endereço? [Dá uma olhada nesse pilar aqui.](https://youtu.be/_CvFy3ypsYc)
5.  Dado que você separou os dados que chegam da request do objeto de domínio, como vai fazer para converter dessa entrada para o domínio? [Sugiro olhar um pouco sobre nossa ideia de Form Value Objects](https://youtu.be/2Oc56btUWQA).
6.  Muitos dos problemas de uma aplicação vem do fato dela trabalhar com objetos em estado inválido. O ponto mais crítico em relação a isso é justamente quando os dados vêm de outra fonte, por exemplo um cliente externo. É por isso que temos o seguinte pilar: quanto mais externa é a borda mais proteção nós temos. Confira uma explicação sobre ele [aqui](https://youtu.be/pu9zErRwk7k) e depois [aqui](https://youtu.be/odzqRwdgVUw)
7.  [Todo framework mvc minimamente maduro possui um mecanismo pronto de realizar validação customizada. Spring, NestJS e ASP.NET Core MVC têm.](https://youtu.be/YXF8Ll64tfk)
8.  Nome,email e descrição são informações obrigatórias. Como você lidou com isso? [Informação natural e obrigatória entra pelo construtor](https://youtu.be/-eVRkz-3nCQ)
9.  Deixamos pistas que facilitem o uso do código onde não conseguimos resolver com compilação. Muitas vezes recebemos String, ints que possuem significados. Um email por exemplo. Se você não pode garantir a validação do formato em compilação, [que tal deixar uma dica para a outra pessoa](https://youtu.be/TqaMn9jTRU0)?
10.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
12.  [Como Alberto faria esse código](https://youtu.be/CghDgad4jWI)?

### **informações de suporte sobre o Spring e JPA**

1.  Para receber os dados da request como json, temos a annotation @RequestBody
2.  Usamos a annotation @Valid para pedir que os dados da request sejam validados
3.  Para realizar as validações padrões existe a Bean Validation
4.  [Como criar um @RestControllerAdvice para customizar o json de saída com erros de validação](https://youtu.be/LlX6zoGwQQA)
5.  [Como externalizar as mensagens de erro no arquivo de configuração.](https://youtu.be/Fsl5E-BGHuU)

