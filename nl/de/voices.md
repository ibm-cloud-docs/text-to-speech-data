---

copyright:
  years: 2019
lastupdated: "2019-07-06"

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

# Sprachen und Stimmen
{: #voices}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} unterstützt eine Vielzahl von Sprachen, Stimmen und Dialekten. Der Service bietet für jede Sprache mindestens eine Frauenstimme an. Für einige Sprachen bietet der Service mehrere Stimmen an, darunter sowohl Männer- als auch Frauenstimmen. Jede Stimme verwendet den geeigneten Tonfall und die passende Satzmelodie für ihren Dialekt.
{: shortdesc}

## Unterstützte Sprachen und Stimmen
{: #languageVoices}

In Tabelle 1 sind die für jede Sprache und jeden Dialekt verfügbaren Stimmen einschließlich des Typs und Geschlechts aufgeführt. Alle Stimmen sind [neuronale Stimmen](#neuralVoices). (Eine neuronale Version der japanischen Stimme ist noch nicht verfügbar.) Falls Sie den optionalen Parameter `voice` in einer Anforderung weglassen, verwendet der Service standardmäßig die Stimme `en-US_MichaelV3Voice`.

<table style="width:100%">
  <caption>Tabelle 1. Unterstützte Sprachen und Stimmen</caption>
  <tr>
    <th style="text-align:left">Sprache</th>
    <th style="text-align:center">Stimme</th>
    <th style="text-align:center">Geschlecht</th>
  </tr>
  <tr>
    <td style="text-align:left">Brasilianisches Portugiesisch</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Kastilisches Spanisch</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Französisch</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Deutsch</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
  <tr>
    <td style="text-align:left">Italienisch</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Lateinamerikanisches Spanisch</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Nordamerikanisches Spanisch</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Britisches Englisch</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td style="text-align:left">Amerikanisches Englisch</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">Weiblich</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">Männlich</td>
  </tr>
</table>

Die Stimmen `es-LA_SofiaV3Voice` und `es-US_SofiaV3Voice` sind im Wesentlichen identisch. Der größte Unterschied besteht in der Interpretation eines Dollarzeichens ($) durch die beiden Stimmen. Die lateinamerikanische Version verwendet den Begriff *pesos*, während die nordamerikanische Version den Begriff *d&oacute;lares* verwendet. Darüber hinaus kann es einige geringere Unterschiede zwischen den beiden Stimmen geben.
{: note}

### Neuronale Stimmen
{: #neuralVoices}

Die neuronale Sprachtechnologie nutzt mehrere Deep Neural Networks (DNNs), um die akustischen (spektralen) Merkmale der Sprache vorherzusagen. Die DNNs werden für eine natürliche menschliche Sprache trainiert und erzeugen die daraus resultierende Audioausgabe aus den vorhergesagten akustischen Merkmalen. Während der Synthese sagen die DNNs die Tonhöhe und die Phonemdauer (Satzrhythmus), die spektrale Struktur und die Signalform der Sprache voraus. Neuronale Stimmen erzeugen Sprache, die klar klingt und eine sehr natürlich klingende und geschmeidige Tonqualität hat. 

Weitere Informationen über die neuronale Sprachtechnologie des Service finden Sie hier:

-   Blogbeitrag [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   Forschungspapier [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

### Stimmenanpassung
{: #customizeVoice}

Bei der synthetischen Erstellung von Sprache aus Text wendet der Service sprachenabhängige Ausspracheregeln an, um die normale Schreibweise eines Wortes in eine phonetische Schreibweise zu konvertieren. Bei gängigen Wörtern funktionieren die Ausspracheregeln des Service gut, jedoch kann es bei unüblichen Wörtern wie beispielsweise Begriffen fremdsprachlichen Ursprungs, Personennamen sowie Abkürzungen oder Akronymen zu mangelhaften Ergebnissen kommen.

Falls das Wörterbuch Ihrer Anwendung solche Wörter enthält, können Sie mit der Anpassungsschnittstelle angeben, wie sie vom Service ausgesprochen werden sollen. Weitere Informationen enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).

Sie erstellen ein benutzerdefiniertes Sprechmodell für eine bestimmte Sprache, nicht für eine bestimmte Stimme. So kann ein benutzerdefiniertes Modell für seine angegebene Sprache mit jeder Stimme verwendet werden.

## Stimme angeben
{: #specifyVoice}

Sowohl die HTTP-Methoden `GET` und `POST /v1/synthesize` als auch die WebSocket-Methode `/v1/synthesize` akzeptieren einen optionalen Abfrageparameter `voice`, mit dem die Stimme für die synthetisch erstellte Audioausgabe angegeben wird. Weitere Informationen enthalten die Abschnitte [HTTP-Schnittstelle](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) und [WebSocket-Schnittstelle](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).

Der Service legt dem Verständnis der Sprache für den Eingabetext die angegebene Stimme zugrunde. Achten Sie darauf, eine Stimme anzugeben, die mit der Sprache des Eingabetextes übereinstimmt. Falls Sie beispielsweise die Stimme für Französisch (`fr-FR_ReneeV3Voice`) angeben, geht der Service davon aus, dass der Eingabetext in Französisch geschrieben ist. Wenn Sie Text übergeben, der nicht in der Sprache der Stimme geschrieben ist (z. B. englischer Text für die französische Stimme), liefert der Service möglicherweise keine sinnvollen Ergebnisse.

## Alle verfügbaren Stimmen auflisten
{: #listVoices}

Die Methode `GET /v1/voices` listet Informationen zu allen verfügbaren Stimmen auf. Sie verwendet keine Argumente und gibt ein JSON-Array namens `voices` zurück. Das Array enthält für jede Stimme ein separates Objekt.

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaV3Voice",
      "language": "en-US",
      "gender": "female",
      "url": "{url}/v1/voices/en-US_LisaV3Voice",
      "description": "Lisa: Weibliche Stimme für amerikanisches Englisch.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": false,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

Die Felder der Objekte 'voice' liefern die folgenden Informationen:

-   Das Feld `name` gibt eine ID für die Stimme an (z. B. `en-US_LisaV3Voice`). Geben Sie diesen Wert für den Parameter `voice` der Methode `/v1/synthesize` an.
-   Das Feld `language` gibt die Sprache und die Region der Sprache an (z. B. `en-US`).
-   Das Feld `gender` gibt an, ob es sich um eine Männerstimme (`male`) oder um eine Frauenstimme (`female`) handelt.
-   Das Feld `url` gibt die URL für die Stimme an.
-   Das Feld `description` bietet eine Kurzbeschreibung der Stimme.
-   Das Feld `customizable` enthält einen booleschen Wert dafür, ob die Stimme mit der Anpassungsschnittstelle des Service angepasst werden kann. (Dieses Feld, das dieselben Informationen wie das Feld `custom_pronunciation` bereitstellt, wird aus Gründen der Abwärtskompatibilität beibehalten.)
-   Das Feld `supported_features` beschreibt die zusätzlichen Servicefunktionen, die von der Stimme unterstützt werden:
    -   Der boolesche Wert für `voice_transformation` gibt an, ob die Stimme mit dem SSML-Element `<voice-transformation>` umgewandelt werden kann. Da die Stimmenumwandlung nicht für neuronale Stimmen unterstützt wird, ist für das Feld immer `false` festgelegt.
    -   Der boolesche Wert für `custom_pronunciation` gibt an, ob die Stimme mit der Anpassungsschnittstelle des Service angepasst werden kann.

## Bestimmte Stimme auflisten
{: #listVoice}

Die Methode `GET /v1/voices` listet Informationen zu einer bestimmten Stimme auf. Sie akzeptiert zwei Parameter.

<table>
  <caption>Tabelle 2. Parameter der Methode <code>voices</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parameter</th>
    <th style="text-align:center; width:12%">Typ</th>
    <th style="text-align:center; width:12%">Datentyp</th>
    <th style="text-align:left">Beschreibung</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Erforderlich</em></td>
    <td style="text-align:center">Pfad</td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Gibt die Stimme an, für die Informationen zurückgegeben werden sollen. Sie
      geben eine Stimme durch ihren Namen an (z. B. <code>en-US_LisaV3Voice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Optional</em></td>
    <td style="text-align:center">Abfrage</td>
    <td style="text-align:center">Zeichenfolge</td>
    <td>
      Stellt die GUID (global eindeutige ID) eines angepassten Sprechmodells
      bereit, das für die Sprache der angegebenen Stimme definiert ist. Wenn Sie eine
      Anpassungs-ID angeben, müssen Sie die Anforderung mit den Berechtigungsnachweisen
      für die Instanz des Service ausführen, der Eigner des angepassten Modells ist.

    </td>
  </tr>
</table>

Wenn Sie den Parameter `customization_id` nicht angeben, gibt die Methode die JSON-Ausgabe für die angegebene Stimme zurück; diese ist identisch mit den Informationen, die für eine Stimme durch die Methode `GET /v1/voices` zurückgegeben werden. Falls Sie einen Wert für `customization_id` angeben, enthält die Ausgabe ein Feld `customization`, in dem Informationen zum angegebenen angepassten Sprechmodell bereitgestellt werden.

```javascript
{
  "name": "en-US_LisaV3Voice",
  "language": "en-US",
  "gender": "female",
  "url": "{url}/v1/voices/en-US_LisaV3Voice",
  "description": "Lisa: Weibliche Stimme für amerikanisches Englisch.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": false,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

Die Attribute des zusätzlichen Feldes `customization` liefern Informationen wie beispielsweise die GUID, den Namen, die Sprache und die Beschreibung des angepassten Sprechmodells. Außerdem zeigen sie die Berechtigungsnachweise des Modelleigners, das Datum und die Uhrzeit für die Erstellung des Modells sowie das Datum und die Uhrzeit für die letzte Änderung des Modells.
