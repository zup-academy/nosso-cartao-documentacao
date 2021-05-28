# Trabalhando com o usuário logado (vai impactar no resto do código) 

### Antes de começar
Por favor descreva como você pretende realizar a implementação deste desafio. Para acessar o formulário [clique aqui](https://forms.gle/rx5cNhg5yXwFCBAf7)

### Problema

Você precisa configurar um mecanismo de autenticação via token, provavelmente com o Spring Security, para permitir o login. Caso queira, é só olhar nesse link [aqui](https://youtu.be/0I--CLsqC7w). Aí tem todo código de segurança necessário para autenticar no Spring Security via token jwt. Fique a vontade para entendê-lo e aplicar no projeto.

Caso você esteja utilizando NestJS, ASP.NET Code MVC ou outro framework, é só decidir por qual tecnologia de segurança você vai querer. 

### Solução que eu faria para focar mais nas features

Em todo trecho de código que precisar do usuário logado, na primeira linha do método do controller, eu buscaria pelo usuário com um email específico e usaria ele como "referência logada" na aplicação.

Depois, se você quiser, é só habilitar o projeto de segurança, receber o usuário como argumento do método e apagar essa linha... Tudo deveria funcionar normalmente.

### Depois de finalizar
Antes de passar para a próxima funcionalidade, envie o link para o diff da sua solução acessando [este formulário](https://forms.gle/QDNTTALDcUSV3hM59)
