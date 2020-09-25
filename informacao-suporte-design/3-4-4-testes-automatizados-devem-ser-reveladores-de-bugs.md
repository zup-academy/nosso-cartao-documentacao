# Criamos testes automatizados para que ele nos ajude a revelar e consertar bugs na aplicação.

Quando olhamos para os testes automatizados construídos em diversos tipos de projetos e perguntamos o motivo daquilo, temos algumas respostas do pool abaixo:

* Segurança para refatorar;
* Quero garantir que o que eu fiz está certo;
* Preciso ter uma documentação executável;
* Segurança para alterar o código em função de um bug (manutenção corretiva);
* Segurança para alterar o código para acrescentar funcionalidades (manutenção evolutiva);
* Aumenta a qualidade do código;

Obviamente existem outras possibilidades de resposta aí nessa lista. Tirando a parte de ter uma documentação executável, muito se fala em segurança e qualidade do código do ponto de vista de confiabilidade de execução e manuntenção. 

## A aposta potencialmente arriscada dos testes automatizadas

Existem algumas coisas que são quase garantidas quando uma equipe decide que o software deve ser coberto por testes automatizados. 

* Mais código será escrito;
* Bugs serão gerados no código de teste;
* O software, como um todo, vai ficar mais complexo pelo olhar de qualquer métrica que você queira;
* Mais código precisará ser mantido;
* Cada funcionalidade vai demorar mais tempo para ser escrita;

Claro que estamos evoluindo muito na área de pesquisa relativa a testes e inclusive já temos projetos que tentam gerar boa parte dos testes automatizados sozinhos. Mas, quando consideramos que é uma pessoa que vai escrever, a lista de cima apresenta uma bela tendência de ser verdade.

O potencial de retorno dessa aposta é o seguinte:

* Pode até demorar mais tempo, mas a qualidade do ponto de vista de confiabilidade de execução vai ser maior. Ou seja, vai apresentar menos falhas de execução;
* Pode até demorar mais tempo, mas a qualidade interna do código vai ser maior;
* Vai ser mais fácil alterar o código no futuro;

O ponto de atenção aqui é: E se você não obtiver este retorno? Como que o código relativo ao teste automatizado pode realmente facilitar a obtenção do retorno?

Do mesmo jeito que você deve se preparar para investir num mercado financeiro de alto risco, você também precisa preparar seus testes para maximixar o potencial de retorno dele. 

Sempre que você tem o lado negativo garantido e o lado positivo em risco, é necessário muito mais esforço para sair do outro lado. É literalmente um objetivo muito desafiador.


## Por que você acha que o teste automatizado te dá segurança para alguma coisa?

Aprofundando no tópico sobre segurança, precisamos fazer um questionamento. Como sabemos que o teste automatizado aumenta a segurança do código quando falamos de suportar refatoração, manutenções etc? Uma pergunta simples que você pode fazer é a seguinte: *Quantas vezes sua suíte de testes revelou um bug no sistema antes dele ter sido percebido em produção?*

**Caso a sua suite de testes não seja reveladora de bugs** é importante que você saiba que seu produto pode estar sendo prejudicado pelo seus testes automatizados. A expectativa de retorno que você tinha passadava pelo aumento de confiabilidade de execução, qualidade interna etc. Só que num cenário onde os testes não revelam bugs e você continua pegando tudo em produção, é como se eles não estivessem dando o retorno esperado.

## Técnicas de teste para que ele seja mais revelador de bugs?

Talvez o primeiro o ponto que precisa ser analisado é: Os testes derivados para o código seguem algum tipo de técnica? Abaixo temos alguns exemplos de possíveis técnicas que podem ser combinadas. 

* Specification-based testing;
* Boundary testing;
* Structural testing;
* Design-by-contract como técnica de self-testing;
* Property-based testing;

Cada uma dessas técnicas contribui para que você crie uma suíte de testes que tenha mais chances de revelar bugs antes que eles virem falhas em produção. Porque uma coisa é certa: O software está com bug, ele só não foi descoberto ainda. 

A ideia é que a equipe responsável por desenvolver o código saiba das técnicas e seja capaz de utilizá-las de forma sistemática. 

Em geral, o que se observa muito no mercado é o uso da técnica *Structural testing*, onde os testes são escritos para cobrir o que for possível das linhas de código geradas durante a implementação. Inclusive é daí que vem todo debate sobre cobertura de código e tudo mais. 

Perceba que escrever os testes em função do código gerado é apenas uma das técnicas que pode ser utilizada para derivas bons casos, imagine se você combinar mais algumas?

## A distorção da cobertura de código

Cobertura de código é uma métrica utilizada no mercado para analisar o número de linhas do código fonte que foram testadas pelo casos de testes automatizados. Alguns exemplos de como você pode olhar a cobertura:

* Por linhas de código no total;
* Por branches(if,else,loops);
* Por branches + condicionais;

Inclusive existem mais possibiliddes. Ainda existe muito sistema que o percentual de cobertura é definido em cima do critério mais básico, que é o de linhas de código no total. 

```java	
	public void validate(Object target, Errors errors) {
		TemCombinacaoUsuarioRestauranteFormaPagamento request = (TemCombinacaoUsuarioRestauranteFormaPagamento) target;
		Usuario usuario = manager.find(Usuario.class, request.getIdUsuario());
		Restaurante restaurante = manager.find(Restaurante.class,
				request.getIdRestaurante());

		boolean podePagar = usuario.podePagar(restaurante,
				request.getFormaPagamento(), regrasFraude);
		if (!podePagar) {
			errors.reject(null,
					"A combinacao entre usuario, restaurante e forma de pagamento nao eh valida");
		}
	}
```
Desconsiderando a indentação do código, temos 6 linhas de instruções. Se o critério de cobertura é apenas por linha e o percentual buscado for por exemplo de 80%, um teste pode ser criado verificando apenas o valor ```true``` para a variável ```podePagar``` e tudo vai estar certo. Isso considerando um cenário básico, imagine num sistema com muito mais fluxos?

Uma solução é obviamente você ir aumentando o percentual de cobertura para forçar que de um jeito ou de outro o teste passe pelas linhas. Só que, um percentual desejado de cobertura vira um objetivo, **e objetivo serve para direcionar esforço**. Agora será trazido um exemplo bem simples para demonstrar o que um objetivo mal setado pode fazer. Considere o seguinte código:

```java
public class TesteCoberturaApplication {

	public void test(boolean a, boolean b) {
		System.out.println("passando aqui 1");
		System.out.println("passando aqui 2");
		System.out.println("passando aqui 3");
		System.out.println("passando aqui 4");
		System.out.println("passando aqui 5");
		System.out.println("passando aqui 6");
		if(a || b) {
			System.out.println( "imprime");
		}
	}

}
```

E agora considere os seguintes testes:

```java
class TesteCoberturaApplicationTests {

	@Test
	@DisplayName("teste com a true")
	void teste1() {
		TesteCoberturaApplication teste = new TesteCoberturaApplication();
		teste.test(true, false);
	}
	
	@Test
	@DisplayName("teste com a false")
	void teste2() {
		TesteCoberturaApplication teste = new TesteCoberturaApplication();
		teste.test(false, false);
	}

}
```
Você acabou de ganhar 100% de código, caso você use instrução por linha. O primeiro teste faz com que o ```if``` avalie a expressão como verdadeira e execute o ```sysout```. O segundo teste faz com que a segunda parte da condição seja exercitada, já que o primeiro parâmetro agora foi como ```false```. O relatório vai dar 100% e o código não testou a combinação de primeiro argumento ```false``` e segundo argumento ```true```. 

Se a cobrança for por cobertura, vai ter cobertura. Agora se o critério usado for ruim, vai ter uma cobertura ruim. E esse resultado não é interessante para ninguém. O software continua frágil, sendo que mais esforço e tempo foram investidos. 

O melhor critério é teste que revele bug. Aqui parece valer a pena uma repetição: **O critério mais poderoso para avaliar os testes é verificar quantos bugs foram revelados antes de irem para produção**. Buscando isso, naturalmente o código ganha os outros benefícios como segurança para refatorar etc. 

## Testes inteligentes

Para fechar, podemos falar de uma suite de testes inteligente. Alguns pontos de atenção:

* Será que se operadores de condição forem invertidos, os testes vão quebrar?
* Posso gerar valores contra meus métodos para tentar explorar mais possibilidades?
* Posso gerar automatizados de forma automática?

Criar suítes de testes reveladoras de bugs virou tema de pesquisa e tem muita gente investindo tempo para facilitar a vida do time de desenvolvimento. Para as perguntas acima, temos alguns tipos de testes que podem ser gerados de forma automática por ferramentas:

* Mutation testing;
* Fuzz testing;
* Search-based testing;

Já existem projetos voltados para essa área e com certeza vale a pena explorar o que por possível. 

* PIT(pitest.org) instrumenta código e gera os mutantes. Será que algum teste vai quebrar? Deveria. 
* JQF(https://github.com/rohanpadhye/JQF) é uma ferramenta para Fuzz Testing que tenta gerar valores interessantes buscando maximizar cobertura de código;
* Diffblue(https://www.diffblue.com/) é um software pago que tenta gerar testes automatizados automaticamente;

Todas podem exploradas visando a criação de um suíte de testes realmente poderosa.

## O caminho para uma suíte de testes poderosa

Ter uma suíte de teste poderosa pode ser um caminho parecido com o seguido pelas empresas na busca de uma estratégia de integração, deploy e delivery contínuo. Não é fácil chegar lá, mas pode valer a pena. 

O que adianta colocar software em produção rápido se ele volta sempre? Se o seu conjunto de testes não busca revelar bugs, você pode estar escrevendo a toa. 










