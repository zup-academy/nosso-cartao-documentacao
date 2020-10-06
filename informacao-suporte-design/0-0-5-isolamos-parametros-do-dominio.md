# Separamos as bordas externas do sistema do seu núcleo. 

**Não ligamos parâmetros de requisição externa com objetos de domínio diretamente, assim como não serializamos objetos de domínio para respostas de API.**

Todo framework web moderno permite que você receba os dados de uma requisição web utilizando uma classe do seu próprio domínio. Exemplo:

```java
@PostMapping
public void novaProposta(Proposta proposta) {

}
```
Essa classe proposta poderia um construtor com argumentos com os mesmos nomes dos parâmetros que vem na requisição.

```java
public class Proposta{
    public Proposta(String email, String nome, String documento) {
        ...
    }
}
```

Ou ela poderia ter um construtor sem argumentos e métodos setters para cada informação necessária. E talvez você esteja se perguntando: Isso é ótimo, qual é o problema?

## A fragilidade do contrato estabelecido

No exemplo recebemos o documento(cpf/cnpj) como um argumento do construtor. Dessa forma, neste momento a aplicação cliente que manda dados para gente, deve estar enviando algo assim:

```json
{
    "email": "alberto@zup...",
    "nome": "Alberto Souza",
    "documento": "00000000001",
}
```
Agora imagine que você mudou o fluxo do recebimento do documento. Em vez de receber no construtor da Proposta você vai receber num segundo momento. Como movimento natural, você vai lá e tira aquele argumento do construtor. Neste exato momento você quebrou o cliente que consome qualquer endpoint que recebe uma proposta, pouco importa qual seja. 

## Genérico x Específico

A classe de domínio permeia a aplicação inteira. Ela nasce para ser utilizada em um ponto e naturalmente vai sendo exigida em outros lugares. Dada as necessidades tal classe pode ir sendo alterada. Como você vai minimizar a chance dessa alteração quebrar quem está consumindo algum endpoint? 

Enquanto a classe de domínio nasce para ser usada na aplicação inteira, os parâmetros para um endpoint nascem para ser usados naquele local específico. Dois endpoints diferentes, por coincidência podem usar os mesmos parâmetros, mas eles ainda são diferentes. Os dados podem vir de formulários diferentes. 

## Crie classes para recebimento de parâmetros

A nossa sugestão é que você sempre crie classes específicas para receber os parâmetros. No nosso exemplo seu código poderia ser:

```java
@PostMapping
public void novaProposta(NovaPropostaRequest request){
 ...
}

```

Existe uma bela chance da classe ```NovaPropostaRequest``` ter detalhes parecidos com a classe ```Proposta``` e está tudo bem. Não precisamos reaproveitar todo pedaço de código que existe. 

Agora, se o código estivesse usando o construtor da classe ```Proposta``` e ele fosse alterado, seu código ia dar problema de compilação. E você pode pensar algo assim: "Ah, mas se eu alterar o construtor da classe ```NovaPropostaRequest``` vai quebrar também!". Vai quebrar sim, mas vai quebrar apenas nesse endpoint :). Parar de funcionar é ruim, mas se a correção tiver sido facilitada o impacto disso é bem menor. 

## De quebra ainda estamos mais seguros

Criar classes específicas para receber os dados, ainda deixa nosso código mais seguro. Ficamos um pouco mais protegidos de um ataque conhecido como [Mass Assignment](https://en.wikipedia.org/wiki/Mass_assignment_vulnerability). 

## Meu código ficou mais complexo

Ficou, é verdade. Dada a nossa ideia, esse código está mais complexo sim. Só que o tradeoff está claro, você aumenta a complexidade para diminuir a fragilidade da API e de quebra ainda ganha mais segurança. Claro que precisamos sempre ficar de olho no limite de complexidade inspirado no CDD e decidido pelo projeto.
