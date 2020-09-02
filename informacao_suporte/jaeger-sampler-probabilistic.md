# Jaeger - Amostragem probabilística

As nossas aplicações enviam as amostragens de traces assíncronamente para o Jaeger, porém essa operação requer recursos 
computacionais, como CPU, memória, disco, etc. Portanto dependendo da volumetria o módulo do Jaeger em sua aplicação pode 
causar perda de performance!

Visando isso o OpenTracing provê várias formas de enviar amostragens, como por exemplo a **probabilística** que envia de 
acordo com o desejado, como por exemplo: 10%, 30%, 50%, etc. 

Demais né! Vamos configurar?

Para configurar a amostragem **probabilística**, precisamos adicionar a seguinte propriedade no arquivo `application.properties`:

```properties
# Para enviar 100%
opentracing.jaeger.probabilistic-sampler.sampling-rate=${JAEGER_SAMPLER:1}

# Para enviar 50%
opentracing.jaeger.probabilistic-sampler.sampling-rate=${JAEGER_SAMPLER:0.5}

# Para enviar 10%
opentracing.jaeger.probabilistic-sampler.sampling-rate=${JAEGER_SAMPLER:0.1}
```

# Dicas de Luram Archanjo

Essa é a abordagem que mais uso, pois, provê inúmeras possibilidades \ flexibilidade.

## Informações de suporte

Gostaria de saber mais sobre a Jaeger? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://www.jaegertracing.io/docs/1.18/#about)