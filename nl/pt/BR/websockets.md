---

copyright:
  years: 2019
lastupdated: "2019-06-24"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# A interface WebSocket
{: #usingWebSocket}

Para sintetizar texto para discurso com a interface do WebSocket do {{site.data.keyword.texttospeechdatafull}} para o {{site.data.keyword.icp4dfull}}, primeiro você estabelece uma conexão com o serviço chamando o seu método `/v1/synthesize`. Em seguida, envie o texto que deve ser sintetizado ao serviço como uma mensagem de texto JSON pela conexão. O serviço encerra automaticamente a conexão do WebSocket quando conclui o processamento da solicitação.
{: shortdesc}

O ciclo de solicitação e resposta sintetizado inclui as etapas a seguir:

1.  [Estabelecer uma conexão](#WSopen).
1.  [Enviar o texto de entrada](#WSsend).
1.  [Receber uma resposta](#WSreceive).

A interface WebSocket aceita entradas idênticas e produz resultados idênticos, como os métodos `GET` e `POST /v1/synthesize` da interface HTTP. No entanto, a interface WebSocket suporta o uso do elemento `<mark>` do SSML para identificar o local de marcadores especificados pelo usuário no áudio. Ele também pode retornar informações de sincronização para todas as cadeias do texto de entrada. Para obter mais informações, consulte [Obtendo sincronizações de palavra](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing).

Os fragmentos de código de exemplo a seguir são gravados em JavaScript e são baseados na API do WebSocket HTML5. Para obter mais informações sobre o protocolo WebSocket, consulte o Internet Engineering Task Force (IETF) [Solicitação de comentários (RFC) 6455](http://tools.ietf.org/html/rfc6455){: external}.
{: note}

## Estabelecer uma conexão
{: #WSopen}

O {{site.data.keyword.texttospeechshort}} usa o protocolo WebSocket Secure (WSS) para tornar o método `/v1/synthesize` disponível no terminal a seguir. Para obter mais informações sobre os componentes da URL, consulte [Fazendo solicitações para o serviço](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests).

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

Os exemplos na documentação referem-se a esse terminal como `{ws_url}`.
{: note}

Um cliente WebSocket chama esse método com os parâmetros de consulta a seguir para estabelecer uma conexão autenticada com o serviço.

<table>
  <caption>Tabela 1. Parâmetros do método <code>/v1/synthesize</code></caption>
  <tr>
    <th style="text-align:left; width:23%">Parâmetro</th>
    <th style="text-align:center; width:12%">Tipo de dados</th>
    <th style="text-align:left">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>access_token</code>
      <br/><em>Obrigatória</em></td>
    <td style="text-align:center">Sequência</td>
    <td style="text-align:left">
      Passe um token de acesso válido para autenticar com o serviço. Deve-se usar o token de acesso antes de sua expiração.
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Especifica a voz na qual o texto deve ser falado no áudio.
      Omita o parâmetro para usar a voz padrão, `en-US_MichaelV3Voice`.
      Para obter mais informações, consulte [Idiomas e vozes](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Especifica o Identificador Exclusivo Global (GUID) para uma voz customizada
      modelo que deve ser usado para a síntese. É garantido que um modelo de voz customizado funcione apenas se ele corresponder ao idioma da voz usada para a síntese. Se você incluir um ID de customização, a solicitação deverá ser realizada com credenciais para a instância do serviço que possui o modelo customizado. Omita o parâmetro para usar a voz especificada sem a customização. Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Sequência</td>
    <td style="text-align:left">
      Associa um ID do cliente aos dados transmitidos pela conexão. O parâmetro aceita o argumento <code>customer_id={id}</code>, em que <code>id</code> é uma sequência genérica ou aleatória que deve ser associada aos dados. Deve-se codificar com URL o argumento para o parâmetro, por exemplo, `customer_id%3dmy_ID`. Por padrão, nenhum ID do cliente está associado aos dados. Para obter mais informações, consulte [Segurança de informações](/docs/services/text-to-speech-data?topic=text-to-speech-data-information-security).
    </td>
  </tr>
</table>

O fragmento de código JavaScript a seguir estabelece uma conexão com o serviço. A chamada para o método `/v1/synthesize` passa os parâmetros de consulta `access_token` e `voice`, o último para direcionar o serviço para usar a voz Allison do inglês dos EUA. Depois que a conexão estiver estabelecida, os listeners de eventos (`onOpen`, `onClose` e assim por diante) serão definidos para responder a eventos do serviço.

```javascript
var my_access_token = '{token}';
var wsURI = '{ws_url}/v1/synthesize'
  + '?access_token=' + my_access_token
  + '&voice=en-US_AllisonV3Voice';
var websocket = new WebSocket(wsURI);

websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

## Enviar o texto de entrada
{: #WSsend}

Para sintetizar o texto, o cliente transmite uma mensagem de texto JSON simples para o serviço com os parâmetros a seguir.

<table>
  <caption>Tabela 2. Parâmetros da mensagem de texto JSON</caption>
  <tr>
    <th style="text-align:left; width:23%">Parâmetro</th>
    <th style="text-align:center; width:12%">Tipo de dados</th>
    <th style="text-align:left">Descrição</th>
  </tr>
  <tr>
    <td><code>text</code><br/><em>Obrigatória</em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Fornece o texto que deve ser sintetizado. O cliente pode transmitir um texto sem formatação ou anotado com o Speech Synthesis
      Markup Language (SSML). O cliente pode transmitir um máximo de 5 KB de texto de entrada com a solicitação. O limite inclui qualquer SSML especificado. Para obter informações adicionais, consulte
     [Especificando Texto de Entrada](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP#input)
      e as seções que o seguem.<br/><br/>
      A entrada do SSML também pode incluir o elemento <code>&lt;mark&gt;</code>.
      Para obter mais informações, consulte [Especificando uma marca do SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing#mark).
    </td>
  </tr>
  <tr>
    <td><code>aceitar</code><br/><em>Obrigatória</em></td>
    <td style="text-align:center">Sequência</td>
    <td>
      Especifica o formato solicitado (tipo MIME) do áudio. Use
      `*/*` para solicitar o formato de áudio padrão, <code>audio/ogg;codecs=opus</code>. Para obter mais informações, consulte [Formatos de áudio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats).
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">String[ ]</td>
    <td>
      Especifica que o serviço deve retornar informações de sincronização de palavra para todas as sequências do texto de entrada. O serviço retorna o horário de início e de término de cada token da entrada. Especifique <code>words</code> como o elemento lone da matriz para solicitar sincronizações de palavra. Especifique uma matriz vazia ou omita o parâmetro para não receber sincronizações de palavra.
      Para obter mais informações, consulte [Obtendo sincronizações de palavra](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing#timing). <em>Não suportado para o texto de entrada em japonês.</em>
    </td>
  </tr>
</table>

O fragmento a seguir do código JavaScript transmite uma mensagem "Hello world" simples como o texto de entrada e solicita o formato padrão para o áudio. As chamadas são incluídas na função `onOpen` definida para o cliente com o objetivo de garantir que sejam enviadas somente após a conexão ser estabelecida.

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

O serviço responde essa mensagem enviando uma mensagem de texto que confirma o formato da resposta de áudio. A resposta a seguir confirma o formato de áudio padrão.

```javascript
{
  'binary_streams': [
    {
      content_type: 'audio/ogg;codecs=opus'
    }
  ]
}
```
{: codeblock}

## Receber uma resposta
{: #WSreceive}

Depois de confirmar o formato de áudio, o serviço envia o áudio sintetizado como um fluxo binário de dados no formato indicado. O serviço envia informações de sincronização como uma ou mais mensagens de texto se

-   O texto de entrada incluir um ou mais elementos `<mark>` do SSML.
-   Você especificar o parâmetro `timings` com a solicitação.

O serviço também pode enviar mensagens de texto com avisos ou erros. Quando conclui a síntese do texto de entrada, o serviço encerra automaticamente a conexão do WebSocket.

O cliente precisa anexar respostas binárias do serviço aos resultados de áudio recebidos por meio da conexão. Ele pode manipular mensagens de texto as respondendo, exibindo ou capturando para uso pelo aplicativo (por exemplo, se contiverem locais de marca). O exemplo simples a seguir de uma função `onMessage` anexa mensagens de texto e binárias recebidas do serviço para a variável apropriada com base em seu tipo. Quando a função `onClose()` é executada, o fluxo de áudio inteiro foi recebido.

```javascript
var messages;
var audioStream;

function onMessage(evt) {
  if (typeof evt.data === string) {
    mensagens + = evt.data;
  } else {
    console.log('Received ' + evt.data.size() + ' binary bytes');
    audioStream += evt.data;
  }
}

function onClose(evt) {
  // The audio stream is complete.
}
```
{: codeblock}

## Códigos de retorno do WebSocket
{: #returnCodes}

O serviço pode enviar os códigos de retorno a seguir para o cliente por meio da conexão do WebSocket:

-   `1000` indica encerramento normal da conexão, o que significa que a finalidade para a qual a conexão foi estabelecida foi atendida.
-   `1002` indica que o serviço está encerrando a conexão devido a um erro de protocolo.
-   `1006` indica que a conexão foi encerrada anormalmente.
-   `1009` indica que o tamanho do quadro excedeu o limite de 4 MB.
-   `1011` indica que o serviço está encerrando a conexão porque encontrou uma condição inesperada que o impede de preencher a solicitação, como um argumento inválido. O código de retorno também pode indicar que o texto de entrada era muito grande.

Se o soquete fechar com um erro, o serviço enviará ao cliente uma mensagem informativa do formulário `{ "erro": "Mensagem de erro específica" }`antes de fechar. O serviço também pode enviar mensagens de aviso não fatais para parâmetros desconhecidos.

## Exemplo de mensagens de erro e de aviso
{: #returnErrors}

Os exemplos a seguir mostram respostas de erro. Incluem uma mensagem de texto JSON e uma mensagem formatada do método de retorno de chamada `onClose` do cliente. As mensagens formatadas iniciam com o booleano `true` porque a conexão está encerrada. Também incluem o código de erro do WebSocket que causou o encerramento.

-   Esse exemplo mostra mensagens de erro para um argumento inválido para o parâmetro `accept`:

    ```javascript
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   Este exemplo mostra mensagens de erro para um parâmetro `text` ausente:

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

O exemplo a seguir mostra uma resposta de aviso, nesse caso, para um parâmetro desconhecido chamado `invalid-parameter`. Ele não inclui a segunda mensagem porque a conexão não foi encerrada pelo aviso.

```javascript
{
  "avisos": "Argumentos desconhecidos: invalid-parameter."
}
```
{: codeblock}

Para obter mais informações sobre os códigos de retorno do WebSocket, consulte o Internet Engineering Task Force (IETF) [Solicitação de comentários (RFC) 6455](http://tools.ietf.org/html/rfc6455){: external}.
