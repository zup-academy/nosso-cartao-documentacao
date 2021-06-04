# Concorrência. VII do 12 Factor Apps

_"Espera um minuto, posso adicionar mais CPU e Memória que meu processo
suporta, isso não é um problema, né?"_

Esse tipo de escalabilidade é chamada de escalabilidade vertical e não é uma prática
recomendada para aplicações de nuvem. Essa prática normalmente tem um limite,
por exemplo, nossa máquina não suporta mais que 64 GB de Ram, perceba que temos um limite,
esse limite impacta diretamente nossa capacidade de escalar aplicações.

A prática recomendada é escalar processos ou escalabilidade horizontal.
Que ao contrário da escalabilidade vertical onde procuramos adicionar mais
recursos como CPU e Memória buscamos criar múltiplos processos com menor consumo
de memória e CPU e distribuir a carga entre eles.

Um exemplo, podemos colocar duas instâncias para atender mais requisições.
Perceba que a prática VI Executar a aplicação como mínimo de estado possível
é muito importante aqui, pois ele impacta diretamente este pilar.

## Informações de suporte

* Talvez você queira o link da documentação oficial, [aqui você pode encontrá-lo](https://12factor.net/pt_br/concurrency) 


