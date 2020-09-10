# Introdução

Bem vindo(a) ao Bootcamp, no qual foi feito com muito carinho para você aprender e evoluir de forma exponencial 
(#aprendizadoAcimaDoPlano), pois afinal somos Zuppers (#ZupperAjudaZupper)!

Imagina que já tenha ouvido falar bastante sobre o Bootcamp e seus objetivos, essa introdução será mais técnica e como 
gostaríamos que seguisse o treinamento, tudo bem? Vamos lá!?

O treinamento foi pensado para trazer um caso real, ou seja, muitas integrações e bastantes desafios 
técnicos te espera, tais como:

- Apache Kafka
- OpenTracing
- Métricas
- Kubernetes

Gostou das tecnologias? Foi apenas uma amostra tem muito mais pela frente!

Nesse treinamento você será responsavél por criar um sistema de cartões, porém no escopo de provisonamento do cartão, 
fatura e extrato, não seremos responsáveis por gerenciar as transações, pois, as mesmas são gerenciadas através de uma 
rede de captura e o nosso sistema somente será notificado via Apache Kafka!

Para que seja possível desenvolver as funcionalidades citadas a acima, precisaremos criar três Microsserviços, sim a 
gente irá trabalhar com arquitetura distrubuída (Microsserviços), que irão em algum momento se integrar com o sistema 
legado, conforme imagem abaixo:

![alt text](/images/big-picture.png "Big Picture")

Está ansioso(a) para começar? Vamos lá!?

O desenvolvimento das funcionalidades devem seguir uma ordem, que deve ser:

1º Desenvolvimento das funcionalidades da Proposta
2º Desenvolvimento das funcionalidades da Transação
3ª Desenvolvimento das funcionalidades da Fatura

> **Você deve seguir a sequência do treinamento, na qual foi pensando com muito carinho, para que você aproveitar ao 
>máximo e aprender gradativamente cada técnica, tecnologia e conceito!**

Cada funcionalidade está seguimentada em pastas:

```text
/proposta
/transacao
/fatura
```

Cada pasta tem seus desafios ordenados, novamente você deve seguir a sequência, como por exemplo:

```text
/proposta
    000.setup_projeto.md
    001.setup_docker_compose.md
    005.criacao_proposta.md
```

Demais né! Está ansioso(a) para codificar?

## TO-DO

Imagem da arquitetura do legado
Link do github do docker-compose
Link do template Java para fazer Fork
Link do template Kotlin para fazer Fork

Restrições:

- Não criar uma transação
- Transações são geradas através de uma rede de captura e nosso sistema somente será notificado via Apache Kafka