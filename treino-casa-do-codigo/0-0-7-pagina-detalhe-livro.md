### **Implementação da página de detalhe**

Precisamos criar uma página com as mesmas informações que encontramos na página de detalhe da Casa do Código. Aqui está a página real => [https://www.casadocodigo.com.br/products/livro-spring-boot](https://www.casadocodigo.com.br/products/livro-spring-boot)

**A ideia aqui é implementar todo código necessário para que tenhamos uma página com quase todas informações da página de detalhe da CDC.**

### **necessidades**

*   Ter um endpoint que em função de um id de livro retorne os detalhes necessários para montar a página.

### **restrições**

*   Se o id não existir é para retornar 404

### **Resultado esperado**

*   que o front possa montar a página

### **sobre a utilização do material de suporte aqui**

Esta é uma feature que reutiliza as habilidades trabalhadas até aqui. Tente implementar sem o uso do material de suporte. 

### **informações de suporte para a feature**

1. Uma pergunta que você pode se fazer aqui é: crio uma classe nova aqui ou apenas adiciono um método em um controller existente. Lembre de conferir a ideia de [Controllers 100% coesos](https://drive.google.com/file/d/10f3lT3lB2CEXdyss7ZjeSVzmDkzEU57d/view?usp=sharing) .
2.  É normal uma mesma classe possuir mais de uma forma de exibição de seus dados no sistema. [Como lidar com isso?](https://drive.google.com/file/d/1hFVUZrwNdqV0W4EY0zYDIm3vUSgJGf4S/view?usp=sharing)
3.  Utilize um insomnia ou qualquer outra forma para verificar o endpoint
4.  [Como Alberto faria esse código?](https://drive.google.com/file/d/1nh8L-NXioQq6B18b1d_SkoqOhffosjcd/view?usp=sharing)

### informações de suporte para a combinação Java/Kotlin + Spring

1.  [Aqui](https://drive.google.com/file/d/16_FGNxrqh3ACLJtSuf7FDaSmekhpoWxE/view?usp=sharing) tem algumas formas de você gerar um status code