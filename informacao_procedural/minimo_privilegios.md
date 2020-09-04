# Como rodar nossa aplicação com o minimo de privilegios necessários???

Provavelmente sua aplicação deve se conectar ou utilizar serviços adicionais para o funcionamento.

Garanta que sua aplicação utilize somente o conjunto de permissões que ela necessita. Exemplo,
se sua aplicação precise de acesso de leitura no banco de dados crie uma conta que permita somente leitura,
não conceda privilégio de escrita sem a real necessidade. Esse tópico garante que nossa aplicação
reduza o espaço ou brechas de segurança.

Essa prática reduz consideravelmente a área possível de ataques, de maneira que nossa aplicação
não seja um ponto de exploração para possíveis ataques.


# Informação de Suporte

- Tem dúvida o que significa área possível de ataque. [Tem um link bem massa aqui](https://cheatsheetseries.owasp.org/cheatsheets/Attack_Surface_Analysis_Cheat_Sheet.html) que explica
o que é isso. Em inglês o termo usado pra isso é **Attack Surface**. Ah... uma dica essa informação vem de uma fonte segura!!!

- O termo em inglês para essa prática é chamado de Principle of Least Privilege (POLP). [Aqui tem uma descrição detalhada sobre o tema](https://digitalguardian.com/blog/what-principle-least-privilege-polp-best-practice-information-security-and-compliance)

- Se você usar **Kubernetes** [aqui vai uma dica](https://kubernetes.io/blog/2018/07/18/11-ways-not-to-get-hacked/#2-enable-rbac-with-least-privilege-disable-abac-and-monitor-logs) de como você pode aplicar o POLP. Uma frase bastante impactante é
>"Incorrect or excessively permissive RBAC policies are a security threat in case of a compromised pod. Maintaining least privilege, and continuously reviewing and improving RBAC rules, should be considered part of the **"technical debt hygiene"** that teams build into their development lifecycle".

