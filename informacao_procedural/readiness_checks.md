# Readiness Check ou Liveness Check


Nossas aplicações normalmente rodam em um ambiente gerenciado, ou seja uma plataforma que é capaz de detectar se alguma coisa não está funcionando conforme o esperado, um crash de aplicação ou carga demasiada.

Nossas aplicações consomem um determinado tempo para estarem aptas a receber um fluxo de trabalho. Durante esse intervalo de tempo é recomendado que nenhuma requisição seja redirecionada para a nossa aplicação em processo de preparação.

Esse processo de preparação pode compreender a configuração de uma fila, conexão com um banco de dados ou um determinado pré-processamento.

Temos algumas alternativas para realizar esta tarefa, quando nossa aplicação expõe uma API REST podemos usar um endpoint *HTTP GET* para esse fim, esse endpoint deve verificar se a aplicação está preparada para começar a receber fluxo de trabalho, ou requisições. Uma vez que a plataforma nota que esse endpoint retorna um status de sucesso, as requisições começam a ser redirecionadas para esta nova instância de serviço.

Processamentos em lote também podem implementar este conceito expondo operações de linha de comando, dessa forma, a plataforma cujo serviço está instalado é capaz de identificar se realmente o serviço está apto a começar o trabalho.

## Dicas

- Tente minimizar o tempo de preparação da sua aplicação sempre que possível. Esse tempo pode impactar sua regra de *auto-scaling* e *alta-disponibilidade* da sua aplicação, pois durante essa fase sua aplicação não pode receber fluxo de trabalho.

- É importante termos um trabalho de ajuste fino nessas configurações, pois elas impactam diretamente suas regras de *alta-disponibilidade* e *auto-scaling*

## Informações de Suporte

- Se você quer descobrir como o **kubernetes** utiliza seu readiness check para garantir que sua aplicação esteja apta para receber fluxo de trabalho. Esse [link](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) vai resolver o seu problema.

- Se você usa o Spring e quer saber como o framework suporta readiness check [acesse aqui!](https://spring.io/blog/2020/03/25/liveness-and-readiness-probes-with-spring-boot)
