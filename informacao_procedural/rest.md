# Padrão REST

A sigla REST significa Representational State Transfer ou em tradução literal Transferência Representacional de Estado que basicamente é um estilo arquitetural
construído para servir aplicações em rede.

### Status Code e descrições

#### 200 - Sucesso

| Status  | Descrição  |
|---|---|
| **200**  | Status genérico de sucesso.  |
| **201**  | Informa que um recurso foi criado com sucesso. Normalmente este recurso é utilizado para responder as requisições do tipo POST.  |
| **202**  | Indica que a requisição foi aceita para um determinado processamento. Este status normalmente é utilizado para requisições assíncronas.  |
| **204**  | Indica que a execução ocorreu com sucesso e que está operação não retornou ou retornará nenhuma informação  |

#### 300 - Redirecionamentos

| Status  | Descrição  |
|---|---|
| **301**  | Indica que a URI solicitada mudou. Nesses casos a nova URI é especificada na resposta.  |
| **302**  | Esse código indica que a URI solicitada foi alterada temporariamente.  |
| **304**  | Resposta utilizada quando há cache envolvido na requisição. Esse status indica que não houve alteração na requisição e ele pode utilizar a versão em cache da resposta.  |

#### 400 - Erros do Cliente

| Status  | Descrição  |
|---|---|
| **400**  | Indica que a URI solicitada mudou. Nesses casos a nova URI é especificada na resposta.  |
| **401**  | O Servidor não reconheceu suas credenciais para o recurso solicitada.  |
| **403**  | Credencial não tem os privilégios suficientes para acessar o recurso solicitado.  |
| **404**  | URI informada não existe.  |
| **405**  | Método HTTP utilizado não é permitido na URI solicitada.  |
| **412**  | Campos da requisição na foram informados ou estão num formato não esperado.  |
| **415**  | Normalmente este erro é ocasionado pela falta do Header Content. Verifique o Header Content-Type ou Content-Encoding.  |
| **422**  | Ocorreu algum erro de negócio com sua mensagem. Sintaticamente a requisição é válida, semanticamente não.  |

#### 500 - Erro no servidor

| Status  | Descrição  |
|---|---|
| **500**  | Indica que o servidor não soube tratar a requisição ou ocorreu erro interno da aplicação.  |
| **502**  | O Proxy ou API Gateway não conseguiu identificar o erro reportado pela aplicação, normalmente um backend.  |
| **503**  | O servidor não pode processar a requisição devido a alguma indisponibilidade.  |

