# Usamos tudo que conhecemos que está pronto. 

A versão completa dessa prática é: **Usamos tudo que conhecemos que está pronto. Só fazemos código do zero se for estritamente necessário.**

Aqui, muito melhor do que ficar explicando, é mostrar o código:

```java
    public class Pagamento {
        //codigo omitido aqui

        public void adicionaTransacoes(List<Transacao> transacoesGeradas) {
            Assert.state(
                    transacoes.stream()
                            .noneMatch(transacao -> transacao
                                    .temStatus(StatusTransacao.concluida)),
                    "Não pode adicionar transacao quando já tem uma marcando que concluiu");

            Assert.state(this.transacoes.addAll(transacoesGeradas),
                    "A transação sendo adicionada já existe no pagamento => "
                            + transacoesGeradas);
                                        
        }        
    }
```

A classe ```Pagamento``` é escrita em Java dentro de um projeto que utiliza o framework *Spring*. A classe ```Assert``` é do próprio *Spring* e está referenciada dentro do ```Pagamento```, que faz parte do domínio da aplicação. 

Uma outra versão deste mesmo código seria a seguinte:

```java
    public class Pagamento {
        //codigo omitido aqui

        public void adicionaTransacoes(List<Transacao> transacoesGeradas) {
            if(transacoes.stream()
                            .anyMatch(transacao -> transacao
                                    .temStatus(StatusTransacao.concluida))){
                        throw new IllegalStateException("Não pode adicionar transacao quando já tem uma marcando que concluiu");
                    }

            if(!this.transacoes.addAll(transacoesGeradas)){
                throw new IllegalStateException("A transação sendo adicionada já existe no pagamento => "
                            + transacoesGeradas);
            }
                                        
        }        
    }
```

Os dois códigos fazem a mesma coisa e poderiam ser escritos, só que no primeiro temos as condicionais omitidas por um método pronto e no segundo temos elas feitas a mão. A depender da métrica de complexidade cognitiva derivada do CDD, você poderia ter algumas variações na pontuação.

* Considera que acoplamento com classes transversais conta ponto, então o uso do ```Assert``` conta 1 ponto de entendimento. 
* Considera que acoplamento com classes transversais não conta ponto, então o uso do ```Assert``` não conta ponto. 
* Considera que branch de código conta ponto, então cada ```if``` vai contar um ponto. No caso, teríamos 2 pontos a mais. 

Vai ser complicado você achar uma métrica, independente se é derivada do CDD, que não leve em consideração o número de branches na verificação de complexidade. 

Ou seja, por que eu vou optar por fazer um código mais complexo sendo que aquilo já está pronto e implementado dentro de uma base de código muito mais madura que a minha?

## O medo do acoplamento do negócio com libs e frameworks

Geralmente o argumento para não acoplar nosso código de domínio com libs e frameworks é que queremos nos proteger de eventuais trocas desses componentes no futuro. 

Caso o futuro reserve uma mudança, vai dar problema de compilação ou execução e trocamos. Será que precisamos ter medo da mudança mesmo? Como mencionamos é da natureza do software mudar de formas que não pensamos, então será que vale a pena mesmo ficar tentando colocar proteções?

## Abrace o acoplamento com tudo que é maduro

Vários frameworks e bibliotecas são muito maduros. Tem tempo de estrada e equipes dedicas para a manutenção e evolução daquilo, é realmente uma frente de trabalho dentro de um negócio. Se aceitamos nos acoplar com frameworks caseiros, muito mais instáveis, por que não vamos nos acoplar com frameworks externos muito mais estáveis? Não parece uma decisão sensata. 

Quanto menos você criar para buscar o objetivo, melhor. Quer dizer que você está chegando lá em cima de bases sólidas e só está investindo tempo no que realmente não existe. 
