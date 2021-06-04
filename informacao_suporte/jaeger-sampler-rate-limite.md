# Jaeger - Amostragem rate limit

As nossas aplicações enviam as amostragens de traces assíncronamente para o Jaeger, porém essa operação requer recursos 
computacionais, como CPU, memória, disco, etc. Portanto dependendo da volumetria o módulo do Jaeger em sua aplicação pode 
causar perda de performance!

Visando isso o OpenTracing provê várias formas de enviar amostragens, como por exemplo a **rate limit** que envia de 
acordo com o desejado por segundo, como por exemplo: 3, 5, 10 operações por segundo.

Demais né! Vamos configurar?

Para configurar a amostragem **rate limit**, precisamos adicionar a seguinte propriedade no arquivo `application.properties`:

```properties
# Para enviar 10 traces por segundo
opentracing.jaeger.rate-limiting-sampler.max-traces-per-second=${JAEGER_SAMPLER:10}
```

## Dicas

Essa é a abordagem mais segura, pois, nunca irá extrapolar o limite e consequentemente não irá impactar sua aplicação.

## Informações de suporte

Gostaria de saber mais sobre a Jaeger? [Aqui tem uma explicação do que entendemos que você deve considerar!](https://www.jaegertracing.io/docs/1.18/#about)
