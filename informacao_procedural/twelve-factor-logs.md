# Logs. XI do 12 Factor Apps

Talvez seu código não está funcionando e está com dificuldade de encontrar o problema, não se preocupe!

Uma das maneiras de se encontrar um erro é por meio de Logs!

Log de dados é um arquivo de texto gerado por um software para descrever eventos sobre o seu funcionamento, 
utilização por usuários ou interação com outros sistemas. Um log, após ser gerado, passa a ser incrementado ao 
longo do tempo com informações que permitem diagnosticar possíveis bugs!

O grande problema é que geralmente os logs são gerados em arquivos e há a necessidade de roteamento dos mesmos!

No 12 Factor Apps nunca devemos nos preocupar com o roteamento ou armazenagem do seu fluxo de saída. Nossa aplicação não 
deve tentar escrever ou gerir arquivos de logs. No lugar, cada aplicação em execução escreve seu próprio fluxo de evento, 
sem buffer, para o **stdout**.



# Informações de suporte

* Talvez você queira o link da documentação oficial!? [Aqui você pode encontrá-lo!](https://12factor.net/pt_br/logs) 