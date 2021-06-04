# Jaeger - Amostragem constante

As nossas aplicações enviam as amostragens de traces assíncronamente para o Jaeger, porém essa operação requer recursos 
computacionais, como CPU, memória, disco, etc. Portanto dependendo da volumetria o módulo do Jaeger em sua aplicação pode 
causar perda de performance!

Visando isso o OpenTracing provê várias formas de enviar amostragens, como por exemplo a **constante** que envia 100% de 
todas as operações processadas pela aplicação para o Jaeger.

Demais né! Vamos configurar?

Para configurar a amostragem **constante**, precisamos adicionar a seguinte propriedade no arquivo `application.properties`:

```properties
# True para enviar 100%
opentracing.jaeger.const-sampler.decision=${JAEGER_SAMPLER:true}

# False para desativar
opentracing.jaeger.const-sampler.decision=${JAEGER_SAMPLER:false}
```

## Dicas

Cuidado com esse tipo de abordagem, pois, quando ligado pode causar uma perda significativa de performance, dependendo 
da quantidade de operações.

## Informações de suporte

Gostaria de saber mais sobre a Jaeger? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://www.jaegertracing.io/docs/1.18/#about)
