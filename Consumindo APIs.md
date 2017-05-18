# [Consumindo APIs disponibilizadas pelo SERPRO](#consumindo)

[O que é _API_?](#o_que_e_api) - [_APIs_ Disponíveis](#apis_disponiveis) - [Degustação e Testes](#degustacao_e_testes) - [Como Consumir os Serviços](#como_consumir_os_servicos) - [Autenticação](#autenticacao) - [Códigos de Erros](#codigos_de_erros) - [Como e Onde Contratar](#como_e_onde_contratar) - [Minha Conta e Estatísticas de Uso](#minha_conta) - [Aplicabilidades](#aplicabilidades)

## O que é _API_?(#o_que_e_api)
Em Inglês o termo _API_ é o acrônimo de _Application Programming Interface_ que significa literalmente Interface de Programação de Aplicativos. Essa interface possibilita que serviços/dispositivos criados com tecnologias diferentes se comuniquem entre si. Eles não precisam saber como o outro dispositivo funciona ou o que ele precisa acessar. Um comando é enviado e em contrapartida é esperado uma resposta que pode ser uma resposta positiva, negativa ou simplesmente informações requeridas. As _APIs_ podem ser utilizadas em diferentes níveis desde a comunicação entre software/hardware e software/software.

Tendo como o exemplo um carro autônomo podemos identificar diferentes níveis de _APIs_ envolvidas em seu funcionamento: Em um nível mais baixo temos as APIs que possibilitam a comunicação entre os sensores externos e comando central do veiculo; temos também as APIs responsáveis pelo envio dos comandos da central inteligente a cada um dos dispositivos eletrônicos do automóvel. Podemos identificar também a importância das APIs na comunicação do carro com diversos sistemas/serviços externos inclusive àqueles disponibilizados através da internet. Todo veiculo, autônomo ou não, necessita de um registro que o autorize a circular em todo o território nacional. Esse registro é chamado de RENAVAN (Registro Nacional de Veículos Automotores). Todos os condutores também necessitam de um registro. Chamamos esse registro de CNH (Carteira Nacional de Habilitação). Tanto o RENAVAN quanto a CNH são gerenciados por sistemas que disponibilizam informações à todos os departamento de Transito e agentes de transito do Brasil por meio de APIs. Um Agente de Transito pode ter qualquer informação, em tempo real, de um determinado veículo. Ele pode identificar se este veiculo está envolvido em alguma ocorrência policial, se esta com todos os impostos e seguro obrigatório quitados além de também identificar qualquer informação do condutor, se está com a habilitação vencida ou até mesmo se está envolvido em alguma ocorrência policial.

As _APIs_ possuem um papel crucial em um mundo cada vez mais conectado e que necessita de informações de forma rápida e segura.

[Voltar ao Topo](#consumindo)

## _APIs_ Disponíveis(#apis_disponiveis)
<div style="display: inline;">
 <img src="https://raw.githubusercontent.com/devserpro/doc/master/logo-consulta-cnpj.png" width="100" style="padding-right: 20px;" />
 <img src="https://raw.githubusercontent.com/devserpro/doc/master/logo-consulta-cpf.png" width="100" />
</div>

[Voltar ao Topo](#consumindo)

## Degustação e Testes(#degustacao_e_testes)
Acesse o [Portal do Desenvolvedor](https://dev.serpro.gov.br) e clique no botão **"Teste APIs"**, conforme figura abaixo:
<div style="text-align: center;">
 <a href="https://dev.serpro.gov.br" target="_blank"><img src="https://github.com/devserpro/doc/blob/master/teste-apis.png?raw=true" width="900" /></a>
</div>
<br />
Uma _modal_ (tela) será aberta para a realização de testes utilizando o _Swagger UI_. Caso queira trocar a _API_, basta clicar na logo da _API_ desejada.
<div style="text-align: center;">
 <a href="https://dev.serpro.gov.br" target="_blank"><img src="https://github.com/devserpro/doc/blob/master/teste-apis-swagger.png?raw=true" width="900" /></a>
</div>

[Voltar ao Topo](#consumindo)

## Como Consumir os Serviços(#como_consumir_os_servicos)

Para consumir os serviços do APIGov é necessário que seja estabelecido um contrato com a área responsável pela _API_. No contrato estão definidos:

Data de inicio e término dos acessos;
Limite de requisições que podem ser feitas em um determinado período (requisições/minuto);
_APIs_ que podem ser acessadas;
Depois de firmado o contrato, você receberá dois códigos (_User Key_ e _Consumer Secret_). Esses códigos servem para identificar o contrato. Sempre que precisar acessar as _APIs_ contratadas será necessário informa-los. Mas a frente vamos demostrar como utilizar esses códigos da obtenção de sua _API_.

Exemplo de código:
```javascript
Consumer Key : uldY78ZMvYm4btC0x3XZLG7ZTsYa
Consumer Secret : WyUeBFCUK7wu1Ko61V7bb7yB2Uoa
```

### Passos para acessar a API
As nossas _APIs_ utiliza o protocolo de autorização _OAUTH2_ para disponibilizar o acesso às _APIs_. No exemplo abaixo estamos utilizando o _GranType Client Credentials_ para requisição de token e acesso a _API_:

#### 1 - Informe os _IPs_ de sua máquina

Por medidas de segurança, precisamos liberar o acesso da sua máquina à nossa infraestrutura. Para isso, é necessário que você informe o IP da máquina que irá consumir a _API_ para o endereço: [apigov@serpro.gov.br](mailto:apigov@serpro.gov.br)

#### 2 - Faça a requisição do _Token_ de acesso

O primeiro passo que deve ser seguido antes de realizar a chamado da _API_ é a requisição do token de Acesso. Esse token tem sua validade definida de acordo com a _API_. Para solicitar o token temporário siga os seguintes passos:

Informe ao Gateway suas Credenciais de Acesso
Faça uma requisição _POST_ ao endereço [https://apigateway.serpro.gov.br/token](https://apigateway.serpro.gov.br/token) informando suas credenciais de acesso informando os seguintes parâmetros:

```javascript
[POST] grant_type=client_credentials
[HEAD] Authorization: Basic base64(Consumer Key:Consumer Secret)
```

Como exemplo podemos fazer essa chamada via _cUrl_ da seguinte forma:

```javascript
curl -k -d "grant_type=client_credentials" -H "Authorization: Basic dWxkWTc4Wk12WW00YnRDMHgzWFpMRzdaVHNZYTpXeVVlQkZDVUs3d3UxS282MVY3YmI3eUIyVW9h" https://apigateway.serpro.gov.br/token
```

A chave informada no exemplo acima "dWxkWTc4Wk12WW00YnRDMHgzWFpMRzdaVHNZYTpXeVVlQkZDVUs3d3UxS282MVY3YmI3eUIyVW9h" é resultado do _BASE64_ da chaves de exemplo: "base64(uldY78ZMvYm4btC0x3XZLG7ZTsYa:WyUeBFCUK7wu1Ko61V7bb7yB2Uoa)"

**Receba o Token**
O _Gateway_ informará as iformações de token no seguinte padrão:

```javascript
 {"scope":"am_application_scope default","token_type":"Bearer","expires_in":3295,"access_token":"c66a7de41c96f7008a0c397dc588b6d7"} 
```

**scope** = Algumas APIs definem escopos diferentes para acessos a diferentes funcionalidades. Por exemplo: clientes com escopo de Leitura podem acessar somente funcionalidades de Leitura, escopo de escrita poderão consultar e incluir novos valores, escopo de deleção poderão consultar, incluir e deletar. Quando a _API_ não possui esse tipo de recurso usa-se o escopo padrão.

**token_type** = Define a forma como o token será enviado. Por padrão utilizamos **_Bearer_**.

**expires_in** = Define o tempo em segundos em que o _token_ expirará. Passado esse tempo será necessário realizar uma nova chamada.

**access_token** = O _token_ a ser enviado durante a requisição.

#### 3 - Faça a requisição à _API_

Cada _API_ possui seus próprios atributos. Para acessá-los consulte a aba Console da _API_ da sua _API_.

No exemplo a baixo vamos utilizar a consulta de CNPJ. Nessa seção é possível visualizar as possíveis respostas que a _API_ pode fornecer.

De posse do _Token_, faça uma requisição via _GET_ ao _gateway_ informando os paramentros da _API_ desejada. Exemplo:

```curl
curl -X GET --header "Accept: application/json" --header "Authorization: Bearer c66a7de41c96f7008a0c397dc588b6d7" "https://apigateway.serpro.gov.br/consulta-cnpj/v1/cnpj/00203517121"
```
No exemplo acima foram utilizados os seguintes parâmetros:

```javascript
[HEADER] Accept: application/json - Informamos que o tipo de dados que estamos requerendo, nesse caso JSON
```

```javascript
[HEADER] Authorization: Bearer c66a7de41c96f7008a0c397dc588b6d7 - Informamos o token recebido
```

```javascript
[GET] https://apigateway.serpro.gov.br/consulta-cnpj/v1/cnpj/0022343434 - chamamos a url da API informando o CNPJ . No caso a url é "consulta-cnpj/v1/cnpj/{numero do CNPJ}"
```

Nesse caso, espera-se que a resposta seja a seguinte:
```javascript
   {
  "cnae_secundarias": [
    {
      "codigo": "string",
      "descricao": "string"
    }
  ],
  "ente_federativo": "string",
  "qt_comprovante": "string",
  "data_situacao_especial": "string",
  "porte": "string",
  "tipo_estabelecimento": "string",
  "telefones": [
    {
      "ddd": "string",
      "numero": "string"
    }
  ],
  "data_abertura": "string",
  "correio_eletronico": "string",
  "qt_certidao": "string",
  "situacao_cadastral": {
    "codigo": "string",
    "motivo": "string",
    "data": "string"
  },
  "nome_empresarial": "string",
  "cnae_principal": {
    "codigo": "string",
    "descricao": "string"
  },
  "capital_social": "string",
  "natureza_juridica": {
    "codigo": "string",
    "descricao": "string"
  },
  "nome_fantasia": "string",
  "situacao_especial": "string",
  "orgao": "string",
  "ni": "string",
  "endereco": {
    "bairro": "string",
    "cep": "string",
    "complemento": "string",
    "municipio": "string",
    "uf": "string",
    "logradouro": "string",
    "numero": "string"
  }
}
```

[Voltar ao Topo](#consumindo)

## Autenticação(#autenticacao)

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

[Voltar ao Topo](#consumindo)

## Códigos de Erros(#codigos_de_erros)

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

[Voltar ao Topo](#consumindo)

## Como e Onde Contratar(#como_e_onde_contratar)
Manifestando o interesse por alguma _API_ já existente ou não, você pode preencher as informações do formulário que pode ser encontrado aqui ou entrar em contato diretamente com a área comercial do SERPRO pelo número **0800-728-2323** ou pelo e-mail: [comercial@serpro.gov.br](mailto:comercial@serpro.gov.br).

[Voltar ao Topo](#consumindo)

## Minha Conta e Estatísticas de Uso(#minha_conta)

[Voltar ao Topo](#consumindo)

## Aplicabilidades(#aplicabilidades)

[Voltar ao Topo](#consumindo)
