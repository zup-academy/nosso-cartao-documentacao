# Tem um bug, o que eu faço?

## Olhando com atenção para a exception

```java
feign.FeignException$NotFound: status 404 reading Integracoes#avalia(NovoDocumentoRequest)
	at feign.FeignException.clientErrorStatus(FeignException.java:165) ~[feign-core-10.4.0.jar:na]
	at feign.FeignException.errorStatus(FeignException.java:141) ~[feign-core-10.4.0.jar:na]
	at feign.FeignException.errorStatus(FeignException.java:133) ~[feign-core-10.4.0.jar:na]
	at feign.codec.ErrorDecoder$Default.decode(ErrorDecoder.java:92) ~[feign-core-10.4.0.jar:na]
	at feign.SynchronousMethodHandler.executeAndDecode(SynchronousMethodHandler.java:151) ~[feign-core-10.4.0.jar:na]
	at feign.SynchronousMethodHandler.invoke(SynchronousMethodHandler.java:80) ~[feign-core-10.4.0.jar:na]
	at feign.ReflectiveFeign$FeignInvocationHandler.invoke(ReflectiveFeign.java:103) ~[feign-core-10.4.0.jar:na]
	at com.sun.proxy.$Proxy88.avalia(Unknown Source) ~[na:na]
	at br.com.zup.nossocartao.novaproposta.CriaNovaPropostaController.cria(CriaNovaPropostaController.java:50) ~[classes/:na]
	at br.com.zup.nossocartao.novaproposta.CriaNovaPropostaController$$FastClassBySpringCGLIB$$ecbfcdfb.invoke(<generated>) ~[classes/:na]
	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:218) ~[spring-core-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.invokeJoinpoint(CglibAopProxy.java:771) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:163) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.proceed(CglibAopProxy.java:749) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:367) ~[spring-tx-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:118) ~[spring-tx-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.proceed(CglibAopProxy.java:749) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:691) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at br.com.zup.nossocartao.novaproposta.CriaNovaPropostaController$$EnhancerBySpringCGLIB$$4a18e2ae.cria(<generated>) ~[classes/:na]
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[na:na]
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62) ~[na:na]
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:na]
	at java.base/java.lang.reflect.Method.invoke(Method.java:567) ~[na:na]
	at org.springframework.web.method.support.InvocableHandlerMethod.doInvoke(InvocableHandlerMethod.java:190) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.method.support.InvocableHandlerMethod.invokeForRequest(InvocableHandlerMethod.java:138) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.mvc.method.annotation.ServletInvocableHandlerMethod.invokeAndHandle(ServletInvocableHandlerMethod.java:105) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.invokeHandlerMethod(RequestMappingHandlerAdapter.java:878) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.handleInternal(RequestMappingHandlerAdapter.java:792) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.mvc.method.AbstractHandlerMethodAdapter.handle(AbstractHandlerMethodAdapter.java:87) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1040) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:943) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:1006) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:909) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:652) ~[tomcat-embed-core-9.0.37.jar:4.0.FR]
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:883) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:733) ~[tomcat-embed-core-9.0.37.jar:4.0.FR]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:231) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:53) ~[tomcat-embed-websocket-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:100) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.springframework.web.filter.FormContentFilter.doFilterInternal(FormContentFilter.java:93) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:201) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:202) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:96) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:541) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:139) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:92) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:74) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:343) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:373) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:65) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:868) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1589) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128) ~[na:na]
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628) ~[na:na]
	at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at java.base/java.lang.Thread.run(Thread.java:830) ~[na:na]

```
Aqui temos a chamada stack trace da exception. Basicamente aí você tem todos pontos do código que foram executados até o momento que o bug aconteceu. Você precisa ficar ninja de olhar para essa pilha e interpretá-la.

Se você for olhando de cima para baixo, em algum momento você vai encontrar uma referência para uma linha do seu código de produção. Na primeira exception temos o seguinte:


```java
at br.com.zup.nossocartao.novaproposta.CriaNovaPropostaController.cria(CriaNovaPropostaController.java:50) ~[classes/:na]
```

Os pontos de invocação do seu código são importantes porque é por ali que deve estar o problema. Sempre encontre o primeiro ponto e vá subindo na pilha. O último ponto de invocação do seu código demarca o exato local onde começou uma sequência de eventos que gerou um bug.

## E onde está o bug?

Um bom chute inicial é imaginar que ele está entre o ponto inicial de invocação do seu código e o ponto final. A matemática é simples aqui: tem mais chance de ter bug no nosso código do que no código do framework :). O framework é impossível de ter bug? Não. Só mais complicado porque ele foi muito mais testado em cenários diferentes do que o nosso próprio código.

## Buscando o problema para a primeira exception

```java
feign.FeignException$NotFound: status 404 reading Integracoes#avalia(NovoDocumentoRequest)
	at feign.FeignException.clientErrorStatus(FeignException.java:165) ~[feign-core-10.4.0.jar:na]
	at feign.FeignException.errorStatus(FeignException.java:141) ~[feign-core-10.4.0.jar:na]
	at feign.FeignException.errorStatus(FeignException.java:133) ~[feign-core-10.4.0.jar:na]
	at feign.codec.ErrorDecoder$Default.decode(ErrorDecoder.java:92) ~[feign-core-10.4.0.jar:na]
	at feign.SynchronousMethodHandler.executeAndDecode(SynchronousMethodHandler.java:151) ~[feign-core-10.4.0.jar:na]
	at feign.SynchronousMethodHandler.invoke(SynchronousMethodHandler.java:80) ~[feign-core-10.4.0.jar:na]
	at feign.ReflectiveFeign$FeignInvocationHandler.invoke(ReflectiveFeign.java:103) ~[feign-core-10.4.0.jar:na]
	at com.sun.proxy.$Proxy88.avalia(Unknown Source) ~[na:na]
	at br.com.zup.nossocartao.novaproposta.CriaNovaPropostaController.cria(CriaNovaPropostaController.java:50) ~[classes/:na]
	at br.com.zup.nossocartao.novaproposta.CriaNovaPropostaController$$FastClassBySpringCGLIB$$ecbfcdfb.invoke(<generated>) ~[classes/:na]
	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:218) ~[spring-core-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.invokeJoinpoint(CglibAopProxy.java:771) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:163) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.proceed(CglibAopProxy.java:749) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:367) ~[spring-tx-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:118) ~[spring-tx-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.proceed(CglibAopProxy.java:749) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:691) ~[spring-aop-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at br.com.zup.nossocartao.novaproposta.CriaNovaPropostaController$$EnhancerBySpringCGLIB$$4a18e2ae.cria(<generated>) ~[classes/:na]
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[na:na]
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62) ~[na:na]
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:na]
	at java.base/java.lang.reflect.Method.invoke(Method.java:567) ~[na:na]
	at org.springframework.web.method.support.InvocableHandlerMethod.doInvoke(InvocableHandlerMethod.java:190) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.method.support.InvocableHandlerMethod.invokeForRequest(InvocableHandlerMethod.java:138) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.mvc.method.annotation.ServletInvocableHandlerMethod.invokeAndHandle(ServletInvocableHandlerMethod.java:105) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.invokeHandlerMethod(RequestMappingHandlerAdapter.java:878) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.handleInternal(RequestMappingHandlerAdapter.java:792) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.mvc.method.AbstractHandlerMethodAdapter.handle(AbstractHandlerMethodAdapter.java:87) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1040) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:943) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:1006) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:909) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:652) ~[tomcat-embed-core-9.0.37.jar:4.0.FR]
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:883) ~[spring-webmvc-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:733) ~[tomcat-embed-core-9.0.37.jar:4.0.FR]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:231) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:53) ~[tomcat-embed-websocket-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:100) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.springframework.web.filter.FormContentFilter.doFilterInternal(FormContentFilter.java:93) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:201) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:119) ~[spring-web-5.2.8.RELEASE.jar:5.2.8.RELEASE]
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:202) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:96) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:541) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:139) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:92) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:74) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:343) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:373) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:65) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:868) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1589) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128) ~[na:na]
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628) ~[na:na]
	at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61) ~[tomcat-embed-core-9.0.37.jar:9.0.37]
	at java.base/java.lang.Thread.run(Thread.java:830) ~[na:na]

```

Fatiando a exception acima, temos o seguinte:

```java
feign.FeignException$NotFound: status 404 reading Integracoes#avalia(NovoDocumentoRequest)
	at feign.FeignException.clientErrorStatus(FeignException.java:165) ~[feign-core-10.4.0.jar:na]
	at feign.FeignException.errorStatus(FeignException.java:141) ~[feign-core-10.4.0.jar:na]
	at feign.FeignException.errorStatus(FeignException.java:133) ~[feign-core-10.4.0.jar:na]
	at feign.codec.ErrorDecoder$Default.decode(ErrorDecoder.java:92) ~[feign-core-10.4.0.jar:na]
	at feign.SynchronousMethodHandler.executeAndDecode(SynchronousMethodHandler.java:151) ~[feign-core-10.4.0.jar:na]
	at feign.SynchronousMethodHandler.invoke(SynchronousMethodHandler.java:80) ~[feign-core-10.4.0.jar:na]
	at feign.ReflectiveFeign$FeignInvocationHandler.invoke(ReflectiveFeign.java:103) ~[feign-core-10.4.0.jar:na]
	at com.sun.proxy.$Proxy88.avalia(Unknown Source) ~[na:na]
	at br.com.zup.nossocartao.novaproposta.CriaNovaPropostaController.cria(CriaNovaPropostaController.java:50) ~[classes/:na]
```

Perceba que o bug estoura lá no Feign, mas será que o problema é mesmo lá? Vamos olhar a mensagem de erro que foi gerada.

```
feign.FeignException$NotFound: status 404 reading Integracoes#avalia(NovoDocumentoRequest)
````
É de fundamental importância que você leia as mensagens de erro. Elas são criadas de modo a facilitar a busca por um bug quando ele acontecer. A mesma ideia vale para seu código quando você programar de forma defensiva. E lembre: O bug vai acontecer!

O que significa *status 404*? Aqui você precisa entender dos status http para que isso signifique algo. [Lembre que já temos material de suporte para isso.](../informacao_suporte/rest-404.md). 

E por que recebemos um 404? Será que foi um bug do próprio Feign? Aqui você precisa ficar atento: o local onde o bug estourou não necessariamente representa a razão do bug em si. 

Se o Feign te retornou uma mensagem bonita é que ele já esperava que aquilo poderia acontecer. Se ele já esperava, não parece que o bug dele :). Quem configurou o endereço de acesso? Será que ele está apontando para o local correto?

Quando Alberto foi inspecionando o código dentro daquela fatia de erro, ele percebeu que tinha configurado o endereço errado.
