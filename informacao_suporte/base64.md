# Como utilizar Base64 em Java?

Nesse tutorial vamos aprender como utilizar Base64 em Java!

Está animado!? Vamos lá!

Primeiro precisamos entender um pouco mais sobre Base64!

Base64 é um algoritmo de codificação que permite transformar qualquer caractere de qualquer idioma em um 
alfabeto que consiste em letras latinas, dígitos e sinais. Com isso podemos converter caracteres especiais como os 
logogramas chineses, emoji e até imagens em uma sequência “legível” (para qualquer computador), que pode ser salvo e/ou 
transferido para qualquer outro lugar. É utilizado frequentemente para transmitir dados binários por meios de 
transmissões que lidam apenas com texto, como por exemplo HTTP.

Eba! Já sabemos o que é Base64, vamos codificar?

Como Base64 é muito utilizado existe uma classe nativa do Java para isto, ela é chamada [Base64](https://docs.oracle.com/javase/9/docs/api/java/util/Base64.html)

Como o Base64 é um algoritmo de codificação, vamos começar codificando uma mensagem?

```java
String mensagem = "Testando Base64";
String mensagemCodificada = Base64.getEncoder().encodeToString(mensagem.getBytes());
System.out.println(mensagemCodificada);
```

Muito intuitivo a classe e os métodos, como por exemplo:

- getEncoder: Estou obtendo um codificador do Base64.
- getDecoder: Estou obtendo um decodificador do Base64.

Vamos decodificar a mensagem?

```java
byte[] decode = Base64.getDecoder().decode(mensagemCodificada.getBytes());
String mensagemDecodificada = new String(decode);
System.out.println(mensagemDecodificada);
```

Pronto! Já sabemos utilizar Base64, demais né!

# Dicas de Luram Archanjo

Não utilize Base64 como uma camada de segurança, pois é utilizado apenas para transferir dados com caracteres especiais, 
como por exemplo, uma chave RSA, etc.

Como é um algoritmo de codificação a mensagem Luram Archanjo, sempre vai ser `THVyYW0gQXJjaGFuam8=`, ou seja, ela pode ser 
aberta por qualquer pessoa em qualquer ferramenta que suporta Base64.

# Informação de Suporte

Quer saber mais sobre Base64, acesse o [link!](https://pt.wikipedia.org/wiki/Base64)