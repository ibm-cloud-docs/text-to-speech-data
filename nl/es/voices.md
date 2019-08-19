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

# Idiomas y voces
{: #voices}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} da soporte a una variedad de idiomas, voces y dialectos. El servicio ofrece al menos una voz femenina para cada idioma. Para algunos idiomas, el servicio ofrece varias voces, tanto masculinas como femeninas. Cada voz utiliza la cadencia y la entonación adecuadas según su dialecto.
{: shortdesc}

## Idiomas y voces soportados
{: #languageVoices}

En la tabla 1 se listan las voces disponibles para cada idioma y dialecto, indicando también el tipo y el género. Todas las voces son [Voces neuronales](#neuralVoices). (Todavía no hay disponible una versión neuronal de la voz japonesa.) Si se omite el parámetro opcional `voice` en una solicitud, el servicio utiliza de forma predeterminada la voz `en-US_MichaelV3Voice`.

<table style="width:100%">
  <caption>Tabla 1. Idiomas y voces soportados</caption>
  <tr>
    <th style="text-align:left">Idioma</th>
    <th style="text-align:center">Voz</th>
    <th style="text-align:center">Género</th>
  </tr>
  <tr>
    <td style="text-align:left">Portugués de Brasil</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Español de España</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Francés</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Alemán</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
  <tr>
    <td style="text-align:left">Italiano</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Español de América Latina</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Español de América del Norte</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglés del Reino Unido</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglés de EE.UU.</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
</table>

Las voces `es-LA_SofiaV3Voice` y `es-US_SofiaV3Voice` son esencialmente la misma voz. La diferencia más significativa se refiere a cómo las dos voces interpretan el signo de dólar ($). La versión latinoamericana utiliza el término *pesos*, mientras que la versión norteamericana utiliza el término *d&oacute;lares*. También puede haber otras diferencias menores entre las dos voces.
{: note}

### Voces neuronales
{: #neuralVoices}

La tecnología de voz neuronal utiliza varias redes neuronales profundas (DNN - Deep Neural Networks) para predecir las características acústicas (espectrales) del habla. Las DNN se basan en el habla humana natural y generan el audio resultante a partir de las características acústicas pronosticadas. Durante la síntesis, las DNN predicen el tono y la duración del fonema (prosodia), la estructural espectral y la forma de onda del habla. Las voces neuronales generan habla que es nítida y clara, con una calidad de sonido muy natural y suave.

Para obtener más información sobre la tecnología de voz neuronal del servicio, consulte

-   La publicación de blog [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   El documento de investigación [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

### Personalización de voces
{: #customizeVoice}

Al sintetizar texto, el servicio aplica reglas de pronunciación dependientes del idioma para convertir la ortografía ordinaria de cada palabra en una ortografía fonética. Las reglas de pronunciación del servicio funcionan bien para las palabras comunes, pero pueden producir resultados imperfectos para palabras inusuales, tales como vocablos extranjeros, nombres personales y abreviaturas o acrónimos.

Si el léxico de la aplicación incluye palabras de este tipo, puede utilizar la interfaz de personalización para especificar cómo los pronuncia el servicio. Para obtener más información, consulte [Comprender la personalización](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).

Se crea un modelo de voz personalizado para un idioma específico, no para una voz específica. Por ello, se puede utilizar un modelo personalizado con cualquier voz para su idioma especificado.

## Especificar una voz
{: #specifyVoice}

Tanto los métodos HTTP `GET` y `POST /v1/synthesize`, como el método WebSocket `/v1/synthesize`, aceptan un parámetro de consulta opcional `voice` para especificar la voz del audio sintetizado. Para obtener más información, consulte [La interfaz HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) y [La interfaz WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).

El servicio basa su comprensión del idioma del texto de entrada en la voz especificada. Asegúrese de especificar una voz que coincida con el idioma del texto de entrada. Por ejemplo, si especifica la voz en francés (`fr-FR_ReneeV3Voice`), el servicio presupone que el texto de entrada está escrito en francés. Si pasa texto que no está escrito en el mismo idioma que la voz (por ejemplo, texto en inglés para una voz en francés), puede ser que el servicio no produzca resultados comprensibles.

## Listado de todas las voces disponibles
{: #listVoices}

El método `GET /v1/voices` muestra información sobre todas las voces disponibles. No toma argumentos y devuelve una matriz JSON denominada `voices`. La matriz incluye un objeto distinto para cada voz.

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaV3Voice",
      "language": "en-US",
      "gender": "female",
      "url": "{url}/v1/voices/en-US_LisaV3Voice",
      "description": "Lisa: American English female voice.",
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

Los campos de los objetos de voz proporcionan la información siguiente:

-   `name` es un identificador para la voz (por ejemplo, `en-US_LisaV3Voice`). Especifique este valor para el parámetro `voice` del método `/v1/synthesize`.
-   `language` especifica el idioma y la región de la voz (por ejemplo, `en-US`).
-   `gender` identifica la voz como `male` (masculina) o `female` (femenina).
-   `url` identifica el URL de la voz.
-   `description` proporciona una breve descripción de la voz.
-   `customizable` es un valor booleano que indica si la voz se puede personalizar con la interfaz de personalización del servicio. (Este campo, que proporciona la misma información que el campo `custom_pronunciation`, se mantiene para la compatibilidad con versiones anteriores).
-   `supported_features` describe las características de servicio adicionales que admite la voz:
    -   `voice_transformation` es un valor booleano que indica si la voz se puede transformar mediante el uso del elemento SSML `<voice-transformation>`. Puesto que la transformación de la voz no recibe soporte para las voces neuronales, el campo siempre es `false`.
    -   `custom_pronunciation` es un valor booleano que indica si la voz se puede personalizar con la interfaz de personalización del servicio.

## Listar una voz específica
{: #listVoice}

El método `GET /v1/voices/{voice}` muestra información sobre una voz específica. Acepta dos parámetros.

<table>
  <caption>Tabla 2. Parámetros del método <code>voices</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parámetro</th>
    <th style="text-align:center; width:12%">Tipo</th>
    <th style="text-align:center; width:12%">Tipo de datos</th>
    <th style="text-align:left">Descripción</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Obligatorio</em></td>
    <td style="text-align:center">Vía de acceso</td>
    <td style="text-align:center">Serie</td>
    <td>
      Identifica la voz para la que se debe devolver información. Para especificar una voz se utiliza su nombre (por ejemplo, <code>en-US_LisaV3Voice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Consulta</td>
    <td style="text-align:center">Serie</td>
    <td>
      Proporciona el identificador exclusivo global (GUID) de un modelo de voz personalizado que se ha definido para el idioma de la voz especificada. Si incluye un ID de personalización, debe realizar la solicitud con las credenciales para la instancia del servicio que posee el modelo personalizado.
    </td>
  </tr>
</table>

Si omite el parámetro `customization_id`, el método devuelve la salida JSON de la voz especificada que es idéntica a la información devuelta para una voz por el método `GET /v1/voices`. Si especifica un `customization_id`, la salida incluye un campo `customization` que proporciona información acerca del modelo de voz personalizado especificado.

```javascript
{
  "name": "en-US_LisaV3Voice",
      "language": "en-US",
      "gender": "female",
      "url": "{url}/v1/voices/en-US_LisaV3Voice",
      "description": "Lisa: American English female voice.",
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

Los atributos del campo adicional `customization` proporcionan información como, por ejemplo, el GUID, el nombre, el idioma y la descripción del modelo de voz personalizado. También muestran las credenciales del propietario del modelo, la fecha y la hora en la que se ha creado el modelo y la fecha y la hora de su última modificación.
