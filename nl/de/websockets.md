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

# WebSocket-Schnittstelle
{: #usingWebSocket}

Um mit der WebSocket-Schnittstelle von {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}, synthetisch Sprache aus Text zu erstellen, stellen Sie zunächst eine Verbindung zum Service her, indem Sie seine Methode `/v1/synthesize` aufrufen. Anschließend senden Sie den Text, aus dem synthetisch Sprache erstellt werden soll, über die Verbindung als JSON-Textnachricht an den Service. Der Service schließt die WebSocket-Verbindung automatisch, wenn die Verarbeitung der Anforderung abgeschlossen ist.
{: shortdesc}

Der Zyklus der Anforderung und Antwort für die synthetische Erstellung beinhaltet die folgenden Schritte:

1.  [Verbindung öffnen](#WSopen)
1.  [Eingabetext senden](#WSsend)
1.  [Antwort empfangen](#WSreceive)

Die WebSocket-Schnittstelle akzeptiert dieselben Eingaben wie die Methoden `GET` und `POST /v1/synthesize` der HTTP-Schnittstelle und erzeugt identische Ergebnisse. Bei der WebSocket-Schnittstelle wird jedoch die Verwendung des SSML-Elements `<mark>` unterstützt, mit dem die Position von benutzerdefinierten Markierungen in der Audioausgabe angegeben werden kann. Außerdem können bei dieser Schnittstelle Taktinformationen für alle Zeichenfolgen des Eingabetextes zurückgegeben werden. Weitere Informationen finden Sie unter [Worttakt abrufen](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing).

Die folgenden Snippets des Beispielcodes sind in JavaScript geschrieben und basieren auf der HTML5-WebSocket-API. Weitere Informationen zum WebSocket-Protokoll finden Sie auf der von der Internet Engineering Task Force (IETF) betriebenen Seite [Request for Comment (RFC) 6455](http://tools.ietf.org/html/rfc6455){: external}.
{: note}

## Verbindung öffnen
{: #WSopen}

{{site.data.keyword.texttospeechshort}} verwendet das WSS-Protokoll (WebSocket Secure), um die Methode `/v1/synthesize` am folgenden Endpunkt verfügbar zu machen. [Anforderungen an den Service senden](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) enthält weitere Informationen zu den Komponenten der URL. 

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

In den Beispielen in der Dokumentation wird dieser Endpunkt als `{ws_url}` bezeichnet.
{: note}

Ein WebSocket-Client ruft diese Methode mit den folgenden Abfrageparametern auf, um eine authentifizierte Verbindung zum Service herzustellen.

<table>
  <caption>Tabelle 1. Parameter der Methode <code>/v1/synthesize</code></caption>
  <tr>
    <th style="text-align:left; width:23%">Parameter</th>
    <th style="text-align:center; width:12%">Datentyp</th>
    <th style="text-align:left">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>access_token</code>
      <br/><em>Erforderlich</em></td>
    <td style="text-align:center">Zeichenfolge</td>
    <td style="text-align:left">
      Übergeben Sie ein gültiges Zugriffstoken zur Authentifizierung beim Service. Sie müssen das Zugriffstoken nutzen, bevor es abläuft.
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Optional</em></td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Gibt die Stimme an, die den Text in der Audioausgabe sprechen soll.
      Lassen Sie den Parameter weg, wenn die Standardstimme `en-US_MichaelV3Voice` verwendet werden soll.
      Weitere Informationen finden Sie unter
      [Sprachen und Stimmen](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Optional</em></td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Gibt die GUID (global eindeutige ID) für ein angepasstes Sprechmodell
      an, das für die Synthese verwendet werden soll. Ein angepasstes
      Sprechmodell funktioniert nur dann, wenn es mit der Sprache
      der Stimme übereinstimmt, die für die Synthese verwendet wird. Wenn Sie eine Anpassungs-ID angeben,
      müssen Sie die Anforderung mit den Berechtigungsnachweisen für die Instanz des Service ausführen,
      der Eigner des angepassten Modells ist. Lassen Sie den Parameter weg, um die angegebene Stimme
      ohne Anpassung zu verwenden. Weitere Informationen enthält der Abschnitt
      [Wissenswertes über die Anpassung](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>Optional</em></td>
    <td style="text-align:center">Zeichenfolge</td>
    <td style="text-align:left">
      Ordnet den Daten, die über die Verbindung übertragen werden, eine
      Kunden-ID zu. Der Parameter akzeptiert das Argument
      <code>customer_id={id}</code>; hierbei steht <code>id</code> für eine
      zufällige oder generische Zeichenfolge, die den Daten zugeordnet werden
      soll. Sie müssen das Argument für den Parameter als URL codieren, z. B.
      `customer_id%3dmy_ID`. Standardmäßig wird den Daten
      keine Kunden-ID zugeordnet. Weitere Informationen finden Sie unter
[Informationssicherheit](/docs/services/text-to-speech-data?topic=text-to-speech-data-information-security).
    </td>
  </tr>
</table>

Das folgende Snippet mit JavaScript-Code öffnet eine Verbindung zum Service. Im Aufruf der Methode `/v1/synthesize` werden die Abfrageparameter `access_token` und `voice` übergeben; letzterer weist den Service an, die Stimme 'Allison' für amerikanisches Englisch zu verwenden. Sobald die Verbindung aufgebaut wurde, sind die Ereignislistener (`onOpen`, `onClose` usw.) so definiert, dass sie auf Ereignisse aus dem Service reagieren.

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

## Eingabetext senden
{: #WSsend}

Um aus Text synthetisch Sprache zu erstellen, übergibt der Client eine einfache JSON-Textnachricht mit den folgenden Parametern an den Service.

<table>
  <caption>Tabelle 2. Parameter der JSON-Textnachricht</caption>
  <tr>
    <th style="text-align:left; width:23%">Parameter</th>
    <th style="text-align:center; width:12%">Datentyp</th>
    <th style="text-align:left">Beschreibung</th>
  </tr>
  <tr>
    <td><code>text</code><br/><em>Erforderlich</em></td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Gibt den Text an, aus dem synthetisch Sprache erstellt werden soll. Der
      Client kann einfachen Text oder mit SSML annotierten Text übergeben. Der Client kann mit der Anforderung Eingabetext in einer Größe von maximal
      5 KB übergeben. Die Begrenzung bezieht jeden gegebenenfalls angegebenen
      SSML-Code ein. Weitere Informationen finden Sie unter
      [Eingabetext
      angeben](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP#input) sowie in den dort folgenden Abschnitten.<br/><br/>
      SSML-Eingabe kann auch das Element <code>&lt;mark&gt;</code> enthalten.
      Weitere Informationen finden Sie unter [SSML-Markup eingeben](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing#mark).
    </td>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Erforderlich</em></td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Gibt das angeforderte Format (MIME-Typ) der Audioausgabe an. Verwenden
      Sie den Wert `*/*`, um das Standardaudioformat
      <code>audio/ogg;codecs=opus</code> anzufordern. Weitere Informationen finden Sie in
      [Audioformate](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats).
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>Optional</em></td>
    <td style="text-align:center">Zeichenfolge[ ]</td>
    <td>
      Gibt an, dass der Service für alle Zeichenfolgen des Eingabetextes
      Worttaktinformationen zurückgeben soll. Der Service gibt die Start-
      und die Endzeit für jedes Token der Eingabe zurück. Geben Sie
      <code>words</code> als einziges Element des Arrays an, um den Worttakt
      anzufordern. Geben Sie ein leeres Array an oder lassen Sie den Parameter
      weg, damit keine Worttaktinformationen empfangen werden.
      Weitere Informationen
      finden Sie unter [Worttakt
      anfordern](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing#timing). <em>Bei Eingabetext in Japanisch wird dieser Parameter
      nicht unterstützt.</em>
    </td>
  </tr>
</table>

Das folgende Snippet mit JavaScript-Code übergibt eine einfache Nachricht 'Hello world' als Eingabetext und fordert das Standardformat für die Audioausgabe an. Die Aufrufe sind in der Funktion `onOpen` enthalten, die für den Client definiert ist; dies stellt sicher, dass sie erst gesendet werden, nachdem die Verbindung hergestellt wurde.

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

Der Service antwortet auf diese Nachricht, indem er eine Textnachricht sendet, die das Format der Audioantwort bestätigt. Die folgende Antwort bestätigt das Standardaudioformat.

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

## Antwort empfangen
{: #WSreceive}

Nachdem der Service das Audioformat bestätigt hat, sendet er die synthetisch erstellte Audioausgabe als binären Datenstrom im angegebenen Format. In den folgenden Fällen sendet der Service Taktinformationen in einer oder mehreren Textnachrichten:

-   Der Eingabetext enthält eines oder mehrere SSML-Elemente `<mark>`.
-   Sie haben zusammen mit der Anforderung den Parameter `timings` angegeben.

Der Service kann außerdem Textnachrichten mit Warnungen oder Fehlern senden. Sobald er die synthetische Erstellung von Sprache aus dem Eingabetext fertiggestellt hat, schließt er die WebSocket-Verbindung.

Der Client muss binäre Antworten vom Service an die Audioergebnisse anhängen, die über die Verbindung empfangen wurden. Er kann Textnachrichten verarbeiten, indem sie beantwortet, angezeigt oder zur Verwendung durch die Anwendung (beispielsweise bei enthaltenen Markierungspositionen) erfasst werden. Das folgende einfache Beispiel einer Funktion `onMessage` hängt vom Service empfangene Text- und Binärnachrichten gemäß ihrem Typ an die entsprechende Variable an. Wenn die Funktion `onClose ()` ausgeführt wird, wurde der gesamte Audiodatenstrom empfangen.

```javascript
var messages;
var audioStream;

function onMessage(evt) {
  if (typeof evt.data === string) {
    messages += evt.data;
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

## WebSocket-Rückgabecodes
{: #returnCodes}

Der Service kann über die WebSocket-Verbindung die folgenden Rückgabecodes an den Client senden:

-   `1000` gibt den normalen Abschluss der Verbindung an. Dies bedeutet, dass der Zweck erfüllt ist, zu dem die Verbindung hergestellt wurde.
-   `1002` gibt an, dass der Service die Verbindung aufgrund eines Protokollfehlers schließt.
-   `1006` gibt an, dass die Verbindung abnormal beendet wurde.
-   `1009` gibt an, dass die Rahmengröße die Begrenzung von 4 MB überschritten hat.
-   `1011` gibt an, dass der Service die Verbindung beendet, weil er eine unerwartete Bedingung festgestellt hat, die die Erfüllung der Anforderung verhindert (z. B. ein ungültiges Argument). Der Rückgabecode kann auch bedeuten, dass der Eingabetext zu umfangreich war.

Falls der Socket mit einem Fehler geschlossen wird, sendet der Service eine Informationsnachricht mit dem Format `{"error": "spezielle_fehlernachricht"}` an den Client, bevor der Schließvorgang stattfindet. Der Service kann auch nicht schwerwiegende Warnungen für unbekannte Parameter senden.

## Beispiele für Fehlernachrichten und Warnungen
{: #returnErrors}

Die folgenden Beispiele zeigen Fehlerantworten. Sie enthalten eine JSON-Textnachricht und eine formatierte Nachricht aus der Callback-Methode `onClose` des Clients. Die formatierten Nachrichten beginnen mit dem booleschen Wert `true`, da die Verbindung geschlossen ist. Sie enthalten außerdem den WebSocket-Fehlercode, der den Abschluss verursacht hat.

-   Dieses Beispiel zeigt Fehlernachrichten über ein ungültiges Argument für den Parameter `accept`:

    ```javascript
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   Dieses Beispiel zeigt Fehlernachrichten über einen fehlenden Parameter `text`:

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

Das folgende Beispiel zeigt eine Warnantwort, in diesem Fall für einen unbekannten Parameter namens `invalid-parameter`. Die zweite Nachricht ist nicht enthalten, weil die Verbindung durch die Warnung nicht geschlossen wird.

```javascript
{
  "warnings": "Unknown arguments: invalid-parameter."
}
```
{: codeblock}

Weitere Informationen zu WebSocket-Rückgabecodes finden Sie auf der von der Internet Engineering Task Force (IETF) betriebenen Seite [Request for Comments (RFC) 6455](http://tools.ietf.org/html/rfc6455){: external}.
