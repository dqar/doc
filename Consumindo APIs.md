# Consumindo APIs disponibilizadas pelo SERPRO

## APIs Disponíveis

## Degustação e Testes

## Autenticação

## Códigos de Erros

- **700700 - API blocked**
  * Esta API foi bloqueada temporariamente. Tente novamente mais tarde ou entre em contato com os administradores do sistema. Invocar uma API que está no estado de ciclo de vida BLOCKED

- **900800 - Message throttled out**
  * O número máximo de solicitações que podem ser feitas para a API dentro de um período de tempo designado foi atingido. Espere um minuto até a próxima chamada. Para solicitar mais requisições entre em contato com a área comercial
  
- **900801 - Hard limit exceeded**
  * Limite máximo da API excedida.Para solicitar mais requisições entre em contato com a área comercial.
  
- **900900 - Unclassified authentication failure**
  * Ocorreu um erro não especificado. A API desejada pode não estar disponível. Entre em contato com a área de Suporte para mais informações.
  
- **900901 - Invalid credentials**
  * Informações de autenticação inválidas. O token informado pode estar expirado ou incorreto.
  
- **900902 - Missing credentials**
  * Não há informações de autenticação fornecidas Acessando uma API sem o cabeçalho Authorization: Bearer
  
- **900905 - Incorrect access token type is provided**
  * O tipo de token de acesso informado não é suportado. Os tipos de token de acesso suportados são tokens de acesso de aplicativo e de usuário.
  
- *900906 - No matching resource found in the API for the given request*
  * A API Solicitada não está disponível ou o nome informado está incorreto
  
- *900907 - The requested API is temporarily blocked*
  * Seu acesso à API Solicitada está temporariamente Bloqueado, entre em contato com o suporte para mais detalhes.
  
- **900908 - Resource forbidden**
  * A API Informada está Cancelada ou o usuário não tem privilegio para acesso à API.
  
- **900909 - The subscription to the API is inactive**
  * Sua subscrição está inativa. Entre em contato com o setor comercial para o desbloqueio.
  
- **900910 - The access token does not allow you to access the requested resource**
  * Não é possível acessar API com o token de acesso fornecido.
  
### Resposta com falha - Credenciais não informadas
O sistema retorna a mensagem de erro abaixo:
```xml
<soapenv:fault xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
   <faultcode xmlns:axis2ns9="http://schemas.xmlsoap.org/soap/envelope/">axis2ns9:Client</faultcode>
   <faultstring>Authentication Failure</faultstring>
   <detail>Required OAuth credentials not provided</detail>
</soapenv:fault>
```
**Solução:**
O parâmetro Authorization não está sendo passado no HEADER ou o parametro está sendo passado de forma incorreta.

### Resposta com falha - Erro no acesso
O sistema retorna a mensagem de erro abaixo:
```xml
<soapenv:fault xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
   <faultcode xmlns:axis2ns10="http://schemas.xmlsoap.org/soap/envelope/">axis2ns10:Client</faultcode>
   <faultstring>Authentication Failure</faultstring>
   <detail>Access failure for API: <nome da="" api="">, version: 1</nome></detail>
</soapenv:fault>
```
**Solução:**
O token informado está inválido.

### Resposta com falha - API Indisponível
O sistema retorna a mensagem de erro abaixo:
```xml
<soapenv:envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
   <soapenv:body>
      <soapenv:fault>
         <faultcode xmlns:axis2ns11="http://schemas.xmlsoap.org/soap/envelope/">axis2ns11:Server</faultcode>
         <faultstring>The requested endpoint is not available.</faultstring>
      </soapenv:fault>
   </soapenv:body>
</soapenv:envelope>
```
**Solução:**
A url da API informada está incorreta ou a API não foi sincronizada corretamente nos servidores. Nesse caso, verifique a url de chamada de API e a versão informada e faça a requisição novamente. Se o erro continuar, espere mais 10 minutos para fazer a chamada. Caso o erro persista entre em contanto com o Suporte do Serpro para analisar o comportamento.

### Resposta com falha - Cliente Inválido
O sistema retorna a mensagem de erro abaixo:
```javascript
{"error":"invalid_client","error_description":"Client Authentication failed."}
```
**Solução:**
Esse erro ocorre quando o usuário não envia uma chave de subscrição válida ou quando não é feito o BASE64 da chave.

## Como e Onde Contratar

## Minha Conta e Estatísticas de Uso

## Aplicabilidades
