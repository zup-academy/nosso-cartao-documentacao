# Então vamos por nossa aplicação para RODAR, como realizar o deployment da nossa aplicação!!!

Quando vamos rodar nossa aplicação precisamos garantir alguns controles, como por
exemplo número de replicas ativas, estratégias de rollback quando há uma falha na nova
versão, suportar regras de auto-scaling quando há pico de carga dentre outros.

O kubernetes provê uma forma mais centralizada de nos ajudar com isso através do elemento
Deployment, que na prática significa controlar um grupo de PODs com características similares.

Por exemplo quando temos uma aplicação de **fatura**, todos os PODs dessa mesma aplicação possuem
as mesmas características, como imagem do container, limites de recursos. Caso seja
necessário realizar alguma operação nesses PODs idealmente gostaríamos que fossem aplicadas
para todos que possuem essa mesma característica.

Neste ponto o elemento Deployment nos ajuda, controlar um grupo de PODs que possuem as mesmas características



# Informação de Suporte
* Você pode estar se perguntando "Ainda não tenho certeza o que é um POD", [este link pode te ajudar a compreender 
    um pouco mais sobre isso](https://kubernetes.io/docs/concepts/workloads/pods/)
