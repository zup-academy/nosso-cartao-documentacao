# Processos. VI do 12 Factor Apps

Mas, minha aplicação não pode ter estado??? 

Parece que eu construo aplicação para lidar com estado, por exemplo, a 
entidade proposta do meu sistema, tem um estado de inativa. Eu não posso mais fazer isso???

Podemos, nossas aplicações são construídas para gerenciar alguns estados, como por exemplo
a proposta, de uma maneira geral esse estado deve ser persistido/armazenado em uma outra 
fonte de dados, nos 12 Fatores chamados de Backing Services.

Aqui, estamos preocupados com os estados temporários que estão armazenados por exemplo
na memória, perceba que se nossa aplicação "morrer" inevitavelmente vamos perder esse dado,
de maneira que outra instância da nossa aplicação não consegue "continuar" o trabalho.  
  
Por exemplo, tudo bem se armazenarmos nossa lista de propostas em um banco de dados,
perceba que nossa aplicação ainda se mantém _stateless_ porque o estado não esta nela,
todo o estado está armazenado no banco de dados.

## Informações de suporte

* Talvez você pode estar se perguntando o que são Backing Services. [Neste link você pode encontrar uma definição sobre](https://12factor.net/backing-services) 
  * Ou ainda estar perguntando, tem outro jeito de eu tentar entender isso. O time do Academy [construiu um material para tentar explicar o que é Backing Services]()

* Se você quer entrar em mais detalhes e entender um padrão que ajuda a resolver esse problema, [você pode encontrar aqui uma descrição sobre Shared Nothing](https://en.wikipedia.org/wiki/Shared-nothing_architecture)


