## Possível código não coeso

```java
  String documento = novaProposaRequest.getDocumento();
  if(ehCpf(documento) || ehCnpj(documento)){
      //faz algo aqui
  }

```
O código tem um smell clássico de falta de coesão e consequentemente vazamento de encapsulamento. E por que isso é ruim? Simplesmente porque você está perdendo chance de dividir responsabilidade do código da melhor maneira possível, que é a divisão que acontece sem a necessidade da criação de um novo arquivo. Este mesmo código poderia ser escrito da seguinte forma:

```java
  if(novaProposaRequest.documentoValido()){
      //faz algo aqui
  }
```

Deixar o comportamento perto do estado é algo que foi imaginado lá na criação da teoria que sustenta a orientaçao a objetos, chamada de [Tipos abstratos de dados](http://cv.znu.ac.ir/afsharchim/lectures/p50-liskov.pdf). Sugerimos fortemente que você preste atenção nisso e maximize a coesão dentro do seu código. 

[Aqui tem um outro texto que pode ajudar a analisar isso de maneira lógica](https://medium.com/@albertosouza_47783/encapsulamento-sob-uma-perspectiva-l%C3%B3gica-3d04016e3f14). [Neste outro texto você encontra mais informações sobre smells comuns](https://medium.com/@albertosouza_47783/como-identificar-a-necessidade-de-dividir-responsabilidade-no-c%C3%B3digo-a9377ca682bf)