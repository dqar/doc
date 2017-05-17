# Consumindo APIs disponibilizadas pelo SERPRO

## O que é _API_?
Em Inglês o termo _API_ é o acrônimo de _Application Programming Interface_ que significa literalmente Interface de Programação de Aplicativos. Essa interface possibilita que serviços/dispositivos criados com tecnologias diferentes se comuniquem entre si. Eles não precisam saber como o outro dispositivo funciona ou o que ele precisa acessar. Um comando é enviado e em contrapartida é esperado uma resposta que pode ser uma resposta positiva, negativa ou simplesmente informações requeridas. As _APIs_ podem ser utilizadas em diferentes níveis desde a comunicação entre software/hardware e software/software.

Tendo como o exemplo um carro autônomo podemos identificar diferentes níveis de _APIs_ envolvidas em seu funcionamento: Em um nível mais baixo temos as APIs que possibilitam a comunicação entre os sensores externos e comando central do veiculo; temos também as APIs responsáveis pelo envio dos comandos da central inteligente a cada um dos dispositivos eletrônicos do automóvel. Podemos identificar também a importância das APIs na comunicação do carro com diversos sistemas/serviços externos inclusive àqueles disponibilizados através da internet. Todo veiculo, autônomo ou não, necessita de um registro que o autorize a circular em todo o território nacional. Esse registro é chamado de RENAVAN (Registro Nacional de Veículos Automotores). Todos os condutores também necessitam de um registro. Chamamos esse registro de CNH (Carteira Nacional de Habilitação). Tanto o RENAVAN quanto a CNH são gerenciados por sistemas que disponibilizam informações à todos os departamento de Transito e agentes de transito do Brasil por meio de APIs. Um Agente de Transito pode ter qualquer informação, em tempo real, de um determinado veículo. Ele pode identificar se este veiculo está envolvido em alguma ocorrência policial, se esta com todos os impostos e seguro obrigatório quitados além de também identificar qualquer informação do condutor, se está com a habilitação vencida ou até mesmo se está envolvido em alguma ocorrência policial.

As _APIs_ possuem um papel crucial em um mundo cada vez mais conectado e que necessita de informações de forma rápida e segura.

## _APIs_ Disponíveis

## Degustação e Testes

## Autenticação

### O que é OAUTH 2
As _APIs_ do SERPRO utilizam por padrão o _OAUTH2_ como autorização de acesso às _APIs_. Esse método consiste na troca de chaves entre o cliente e o APIGOV. Inicialmente o cliente informa suas credenciais para receber o token de acesso temporario que deverá ser enviada juntamente com a requisição da _API_. Para saber mais informações sobre o _OAUTH2_ consulte aqui .

Cada subscrição possui uma identificação única composta por duas Chaves que devem ser informadas durante a requisição do token de acesso. O processo de geração de chaves no APIGov pode ver vizualizado em "Como consumir serviços".

O _OATH2_ possui grantypes que são formas diferentes de obter o token de acesso. Por Padrão estamos usando o _Client Credentials_.

### JWT (JSON Web Token)
Conforme descrito em [JWT.IO](https://jwt.io/introduction), _JSON Web Token (JWT)_ é um padrão aberto (_RFC_ 7519) que define um modo compacto que pode ser enviado de diversas formas em uma requisição (nas nossas APIs recebemos via _HEADER_) e auto-contido, cujo o conteúdo é suficiente de identificar a autenticidade da mensagem, utilizadotransmitir com segurança informações entre dois serviços utilizando um objeto _JSON_. Essas informações podem ser verificadas e confiáveis ​​porque são assinadas digitalmente.

Os _JWTs_ podem ser assinados usando um segredo (com o algoritmo _HMAC_) ou um par de chaves público / privado usando o _RSA_.

#### A Estrutura do JWT
O JWT é composto por três partes divididas por uma delimitador (.):

- A primeira é o **_Header_**: Geralmente possui duas partes: a informação do algorítimo que está sendo utilizado e o tipo do Token. Ex.:
```javascript
{
  "alg": "HS256",
  "typ": "JWT"
}
```
- A segunda é o **Corpo**: Contém informações sobre o usuário e metadados adicionais. Essas informações são chamadas de _Claim_. Existem três tipos de _Claim_: reservadas (parâmetros pré-definidos, recomendados mas não obrigatórios), publicas (definição livre) e privadas (definições personalizadas). Ex.:
```javascript
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```
- A terceira é a Assinatura: Consiste no resultado BASE64 do conteúdo do cabeçalho mais o resultado _BASE64_ do conteúdo do corpo criptografado utilizando o algoritmo informado no cabeçalho. No caso do exemplo acima o algorítimo _HS256_ possibilita o uso de uma chamada chave, desta forma a assinatura deve ser conforme descrito abaixo:
```javascript
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  <frase secreta="">)
```

Já o Algorítimo _RSASHA256_ permite que seja utilizado um certificado digital na validação do usuário. Ele verifica a validade da assinatura gerada com chave pública informando a chave pública e privada. Ex.:
```javascript
RSASHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
   -----BEGIN PUBLIC KEY-----  XXX-----END PUBLIC KEY-----  ,
   -----BEGIN RSA PRIVATE KEY----- XXX  -----END RSA PRIVATE KEY-----
```

Todas essas três partes devem ser codificadas em BASE64 da seguinte forma:

BASE64(header).BASE64(corpo).BASE(assinatura)

O resultado dessa combinação seria:

```javascript
ew0KICAiYWxnIjogIkhTMjU2IiwNCiAgInR5cCI6ICJKV1QiDQp9.ew0KICAic3ViIjogIjEyMzQ1Njc4OTAiLA0KICAibmFtZSI6ICJKb2huIERvZSIsDQogICJhZG1pbiI6IHRydWUNCn0=.SE1BQ1NIQTI1NigNCiAgYmFzZTY0VXJsRW5jb2RlKGhlYWRlcikgKyAiLiIgKw0KICBiYXNlNjRVcmxFbmNvZGUocGF5bG9hZCksDQogIDxmcmFzZSBzZWNyZXRhPik=
```

Nas _APIs_ o _JWT_ pode ser usado tanto por parte do cliente que está consumindo a _API_ quanto no envio da informação do usuário à _API_ pelo SERPRO.

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
  
- **900906 - No matching resource found in the API for the given request**
  * A API Solicitada não está disponível ou o nome informado está incorreto
  
- **900907 - The requested API is temporarily blocked**
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
