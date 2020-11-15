# Controllers 100% coesos

## Um aviso antes de consumir este material

O conteúdo aqui usa como base uma linha de design de código que tenta dividir responsabilidade focando em facilitar o entendimento. Fique tranquilo(a) em relação a esta parte neste momento, não estudamos isso ainda e não é necessário que você domine. Foque apenas na linha de manter classes como controllers as mais coesas possíveis. 

## Agora você pode consumir o material

Para assistir este conteúdo em vídeo, clique [aqui](https://drive.google.com/file/d/10f3lT3lB2CEXdyss7ZjeSVzmDkzEU57d/view?usp=sharing). 

​Aqui é explicado um pattern derivado do design de código orientado a entendimento que chamamos de **Controllers 100% coesos.** 

​A ideia é que todo controller, por ser uma classe sem estado inteligente(atributos de dependência), seja 100% coeso. A ideia é que todos os atributos sejam utilizados por todos os métodos que são configurados para lidar com requisições para a aplicação. Perceba que não tem nada a ver com ter apenas um método. Você pode ter quantos quiser, portanto que respeite a restrição da coesão + limite de pontuação máxima para classes sem estado inteligente.

Claro que em casos como o do Spring, onde a configuração da validação customizada é feita através de um método extra no próprio controller, quebra um pouco a coesão, mas a sugestão ainda vale.  ps: você pode ler um pouco mais sobre coesão [aqui](https://www.aivosto.com/project/help/pm-oo-cohesion.html#LCOM1)​.