---

copyright:
  years: 2019, 2020
lastupdated: "2020-11-30"

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

# Languages and voices
{: #voices}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} supports a variety of languages, voices, and dialects. The service offers at least one female voice for each language. For some languages the service offers multiple voices, including both male and female voices. Each voice uses appropriate cadence and intonation for its dialect.
{: shortdesc}

## Supported languages and voices
{: #languageVoices}

Table 1 lists and provides audio samples for the voices that are available for each language and dialect. All voices are [Neural voices](#neuralVoices). If you omit the optional `voice` parameter from a synthesis request, the service uses `en-US_MichaelV3Voice` by default.

| Language | Gender / Type | Voice | Sample |
|----------|:-------------:|:-----:|:------:|
| Brazilian<br/>Portuguese | Female | `pt-BR_IsabelaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/IsabelaV3.wav" type="audio/wav"></audio> |
| English<br/>(United Kingdom) | Female | `en-GB_CharlotteV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/CharlotteV3.wav" type="audio/wav"></audio> |
| | Male | `en-GB_JamesV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/JamesV3.wav" type="audio/wav"></audio> |
| | Female | `en-GB_KateV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/KateV3.wav" type="audio/wav"></audio> |
| English<br/>(United States) | Female | `en-US_AllisonV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/AllisonV3.wav" type="audio/wav"></audio> |
| | Female | `en-US_EmilyV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/EmilyV3.wav" type="audio/wav"></audio> |
| | Male | `en-US_HenryV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/HenryV3.wav" type="audio/wav"></audio> |
| | Male | `en-US_KevinV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/KevinV3.wav" type="audio/wav"></audio> |
| | Female | `en-US_LisaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LisaV3.wav" type="audio/wav"></audio> |
| | Male | `en-US_MichaelV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/MichaelV3.wav" type="audio/wav"></audio> |
| | Female | `en-US_OliviaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/OliviaV3.wav" type="audio/wav"></audio> |
| French | Male | `fr-FR_NicolasV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/NicolasV3.wav" type="audio/wav"></audio> |
| | Female | `fr-FR_ReneeV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/ReneeV3.wav" type="audio/wav"></audio> |
| German | Female | `de-DE_BirgitV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/BirgitV3.wav" type="audio/wav"></audio> |
| | Male | `de-DE_DieterV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/DieterV3.wav" type="audio/wav"></audio> |
| | Female | `de-DE_ErikaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/ErikaV3.wav" type="audio/wav"></audio> |
| Italian | Female | `it-IT_FrancescaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/FrancescaV3.wav" type="audio/wav"></audio> |
| Japanese | Female | `ja-JP_EmiV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/EmiV3.wav" type="audio/wav"></audio> |
| Spanish<br/>(Castilian) | Male | `es-ES_EnriqueV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/EnriqueV3.wav" type="audio/wav"></audio> |
| | Female | `es-ES_LauraV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/LauraV3.wav" type="audio/wav"></audio> |
| Spanish<br/>(Latin American) | Female | `es-LA_SofiaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/SofiaV3.wav" type="audio/wav"></audio> |
| Spanish<br/>(North American) | Female | `es-US_SofiaV3Voice` | <audio controls style="width:250px;height:30px"><source src="https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-neural/SofiaV3.wav" type="audio/wav"></audio> |
{: caption="Table 1. Supported languages and voices"}

The Spanish Latin American and North American `Sofia` voices are essentially the same voice. The most significant difference concerns how the two voices interpret a $ (dollar sign). The Latin American version uses the term *pesos*, while the North American version uses the term *d&oacute;lares*. Other minor differences might also exist between the two voices.
{: note}

### Neural voices
{: #neuralVoices}

Neural voice technology uses multiple Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech. The DNNs are trained on natural human speech and generate the resulting audio from the predicted acoustic features. During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. Neural voices produce speech that is crisp and clear, with a very natural-sounding and smooth audio quality.

For more information about the service's neural voice technology, see

-   The blog post [{{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}}: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   The research paper [High quality, lightweight and adaptable  {{site.data.keyword.texttospeechshort}} using LPCNet](https://arxiv.org/abs/1905.00590){: external}

### Customization
{: #customizeVoice}

When you synthesize text, the service applies language-dependent pronunciation rules to convert the ordinary spelling of each word to a phonetic spelling. The service's pronunciation rules work well for common words, but they can yield imperfect results for unusual words, such as terms with foreign origins, personal names, and abbreviations or acronyms.

If your application's lexicon includes such words, you can use the customization interface to specify how the service pronounces them. For more information, see [Understanding customization](/docs/text-to-speech-data?topic=text-to-speech-data-customIntro).

You create a custom model for a specific language, not for a specific voice. So a custom model can be used with any voice for its specified language. For example, a custom model that you create for the `en-US` language can be used with any US English voice. It cannot, however, be used with an `en-GB` voice.

## Specifying a voice
{: #specifyVoice}

Both the HTTP `GET` and `POST /v1/synthesize` methods, as well as the WebSocket `/v1/synthesize` method, accept an optional `voice` query parameter to specify the voice for the synthesized audio. For more information, see [The HTTP interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingHTTP) and [The WebSocket interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).

The service bases its understanding of the language for the input text on the specified voice. Be sure to specify a voice that matches the language of the input text. For example, if you specify the French voice, `fr-FR_ReneeV3Voice`, the service expects to receive input text that is written in French. If you pass text that is not written in the language of the voice (for example, English text for the French voice), the service might not produce meaningful results.

## Listing all available voices
{: #listVoices}

The `GET /v1/voices` method lists information about all available voices. It takes no arguments and returns a JSON array that is named `voices`. The array includes a separate object for each voice.

The order in which the service returns voices can change from call to call. Do not rely on an alphabetized or static list of voices. Because the voices are returned as an array of JSON objects, the order has no bearing on programmatic uses of the response.

The following example lists all voices that are supported by the service:

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/voices"
```
{: pre}

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
    {
      "name": "es-LA_SofiaV3Voice",
      "language": "es-LA",
      "customizable": true,
      "gender": "female",
      "url": "{url}/v1/voices/es-LA_SofiaV3Voice",
      "supported_features": {
        "voice_transformation": false,
        "custom_pronunciation": true
      },
      "description": "Sofia: Latin American Spanish (español latinoamericano) female voice."
    },
    {
      "name": "pt-BR_IsabelaV3Voice",
      "language": "pt-BR",
      "customizable": true,
      "gender": "female",
      "url": "{url}/v1/voices/pt-BR_IsabelaV3Voice",
      "supported_features": {
        "voice_transformation": false,
        "custom_pronunciation": true
      },
      "description": "Isabela: Brazilian Portuguese (português brasileiro) female voice."
    },
    . . .
  ]
}
```
{: codeblock}

The fields of the voice objects provide the following information:

-   `name` is an identifier for the voice (for example, `en-US_LisaV3Voice`). Specify this value for the `voice` parameter of the `/v1/synthesize` method.
-   `language` specifies the language and region of the voice (for example, `en-US`).
-   `gender` identifies the voice as `male` or `female`.
-   `url` identifies the URL for the voice.
-   `description` provides a brief description of the voice.
-   `customizable` is a boolean value that indicates whether the voice can be customized with the service's customization interface. (This field, which provides the same information as the `custom_pronunciation` field, is maintained for backward compatibility.)
-   `supported_features` describes the additional service features that are supported by the voice:
    -   `voice_transformation` is a boolean value that indicates whether the voice can be transformed by using the SSML `<voice-transformation>` element. Because voice transformation is not supported for neural voices, the field is always `false`.
    -   `custom_pronunciation` is a boolean value that indicates whether the voice can be customized with the service's customization interface.

## Listing a specific voice
{: #listVoice}

The `GET /v1/voices/{voice}` method lists information about a specific voice. It accepts two parameters.

-   `voice` (path parameter, *required* string) - Identifies the voice for which information is to be returned. You specify a voice by its name (for example, `en-US_LisaV3Voice`).
-   `customization_id` (query parameter, *optional* string) - Provides the globally unique identifier (GUID) of a custom model that is defined for the language of the specified voice. If you include a customization ID, you must make the request with credentials for the instance of the service that owns the custom model.

If you omit the `customization_id` parameter, the method returns JSON output for the specified voice that is identical to the information returned for a voice by the `GET /v1/voices` method. If you specify a `customization_id`, the output includes a `customization` field that provides information about the specified custom model.

The following example returns information about the `en-US_LisaV3Voice` and the specified custom model:

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/voices/en-US_LisaV3Voice?customization_id=64f4807f-a5f1-5867-924f-7bba1a84fe97"
```
{: pre}

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

The attributes of the additional `customization` field provide information such as the GUID, name, language, and description of the custom model. They also show the credentials of the model's owner, the date and time at which the model was created, and the date and time of its last modification.
