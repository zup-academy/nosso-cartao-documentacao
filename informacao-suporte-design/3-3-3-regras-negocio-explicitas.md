# Regras de negócio devem ser declaradas de maneira explícita na nossa aplicação.

Aqui é um pilar mais simples, porém importante. Nas nossas aplicações temos requisitos que são funcionais e aqueles não funcionais. Os funcionais, em geral, estão relacionadas as lógicas que precisam ser automatizadas dentro da aplicação. 

Imagine o cenário onde precisamos enviar emails entre outras coisas após o processamento de uma compra.

```java
	private void processa(Long idCompra,RetornoGatewayPagamento retornoGatewayPagamento) {		
		Compra compra = manager.find(Compra.class, idCompra);
		compra.adicionaTransacao(retornoGatewayPagamento);		
		manager.merge(compra);		
		
	}
```

A depender das tecnologias sendo usadas para suportar a construção da aplicação, você pode ter algumas maneiras de resolver isso. Por exemplo, o código acima é escrito em Java e utiliza o Hibernate e o Spring como frameworks de sustentação. Poderíamos ter o seguinte código:

```java
    public class Compra {
        //atributos e outros métodos omitidos

        @PostUpdate
        public void postUpdate(){
            ApplicationContext ctx = //carrega o objeto do spring aqui
            ctx.publish(new EventoPagamentoProcessado(this));
        }
    }
```

O código exibido acima pode causar estranheza por conta do acesso a objetos do Spring dentro do contexto de domínio. Se você já leu o pilar relativo a **Usamos tudo que conhecemos que está pronto**, vai lembrar que não temos medo de nos acoplarmos com frameworks. Esta mesma prática é suportada em outras linguagens com outros frameworks, como Ruby e Rails e Typescript com NestJS :). **O problema é a falta de clareza no fluxo de negócio.**

Quando olhamos para o código de fluxo de novo, como vamos saber que existe um fluxo de processamento de pagamento?

```java
	private void processa(Long idCompra,RetornoGatewayPagamento retornoGatewayPagamento) {		
		Compra compra = manager.find(Compra.class, idCompra);
		compra.adicionaTransacao(retornoGatewayPagamento);		
		manager.merge(compra);				
	}
```

Geralmente aceitamos a falta de clareza em requisitos que não tem a ver com a regra de negócio em si. 

* É necessário logar em modo de tracing toda entrada e saida de método;
* É necessário adicionar um correlation id para toda chamada num ecossistema de microserviços
* É necessário verificar o tempo todo se o usuário está logado para acessar tal ponto;
* É necessário fazer profile para pegar tempo de execução de métodos;

## Dando um passo na clareza do fluxo de negócio

O mesmo fluxo de negócio citado poderia ser escrito da seguinte forma:

```java
	private void processa(Long idCompra,RetornoGatewayPagamento retornoGatewayPagamento) {		
		Compra compra = manager.find(Compra.class, idCompra);
		compra.adicionaTransacao(retornoGatewayPagamento);		
		manager.merge(compra);	
        applicationContext.publish(new EventoPagamentoProcessado(compra));		
	}
```

Agora está claro que existe um processamento para compras que tiveram seus pagamentos processaos por algum gateway. A pergunta que fica é: quais processamentos?

## O ponto de atenção do acoplamento extramente fraco

Sempre falamos de acoplamento fraco e coesão forte. Só que de vez em quando deixamos o acoplamento tão fraco que não conseguimos nem saber onde é que estão as coisas. 

```java
	private void processa(Long idCompra,RetornoGatewayPagamento retornoGatewayPagamento) {		
		Compra compra = manager.find(Compra.class, idCompra);
		compra.adicionaTransacao(retornoGatewayPagamento);		
		manager.merge(compra);	
        applicationContext.publish(new EventoPagamentoProcessado(compra));		
	}
```

Neste código, quem processa o ```EventoPagamentoProcessado```? Um caso parecido acontece quando usamos brokers de mensageria. Só que ela estamos apostando em ganhar tratamento assíncrono, escalabilidade e a resiliência provida pelo broker. Aqui estamos apenas utilizando uma abstração simples do próprio framework, no caso o Spring. 

## Explicitando o acoplamento

Para este tipo de caso, pode ser útil deixar o código um pouco mais acoplado e criar sua própria abstração. 

```java
	private void processa(Long idCompra,RetornoGatewayPagamento retornoGatewayPagamento) {		
		Compra compra = manager.find(Compra.class, idCompra);
		compra.adicionaTransacao(retornoGatewayPagamento);		
		manager.merge(compra);	
        eventosNovaCompra.processa(compra);	
	}

    @Service
    public class EventosNovaCompra {

        @Autowired        
        private Set<EventoCompraSucesso> eventosCompraSucesso;

        public void processa(Compra compra) {
            
            if(compra.processadaComSucesso()) {            
                eventosCompraSucesso.forEach(evento -> evento.processa(compra));
            } 
            else {
                eventosCompraFalha.forEach(evento -> evento.processa(compra));
            }		
        }

    }
```

No ponto do fluxo, mantemos a complexidade igual, já que trocamos a referência para ```EventoPagamentoProcessado``` por ```EventosNovaCompra```. Só que agora temos um caminho claro que pode ser seguido para você a próxima pessoa saber exatamente onde a próxima lógica está acontecendo.

Deixando claro, nossa solução de eventos caseira, principalmente do ponto de vista de resiliência, é frágil também. Só que deixamos a complexidade similar no ponto de invocação e ganhamos clareza, o que pode ser interessante. Nenhuma das duas, porém, se compara em resiliência e escalabilidade com a utilização de um broker de mensageria mais robusto. 



