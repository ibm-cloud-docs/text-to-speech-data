---

copyright:
  years: 2019, 2020
lastupdated: "2020-10-21"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:beta: .beta}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Service features
{: #service-features}

You can access the capabilities of {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} via an HTTP or WebSocket interface. Both interfaces provide features that let you submit and receive different information from the service. And as with all {{site.data.keyword.watson}} services, SDKs are available to simplify application development in many programming languages.
{: shortdesc}

You authenticate to the {{site.data.keyword.texttospeechshort}} service by passing an access token with each request. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} is a multi-tenant cloud solution. Your credentials provide access only to your data, and your data is isolated from other users.

## Synthesizing speech with the service
{: #features-synthesis-interfaces}

The  {{site.data.keyword.texttospeechshort}} service offers an HTTP Representational State Transfer (REST) interface and a WebSocket interface:

-   [The HTTP interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingHTTP) provides both `GET` and `POST` versions of the service's `/v1/synthesize` method. The two versions of the method offer generally equivalent functionality. You pass the text that is to be synthesized as a query parameter with the `GET` method and as the body of the request with the `POST` method.
-   [The WebSocket interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) provides a `/v1/synthesize` method. You pass the text that is to be synthesized over an established WebSocket connection.

With both the HTTP and WebSocket interfaces, you specify the language and voice that are to be used, and the format for the audio that is to be returned.

-   For an overview of the features that are available for speech synthesis, see [Using speech synthesis features](#features-synthesis).
-   For detailed descriptions and examples of the speech synthesis methods, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech-data){: external}.

### Data limits
{: #features-data-limits}

The interfaces accept the following maximum amounts of text with a single request:

-   The HTTP `GET /v1/synthesize` method accepts a maximum of 8 KB of input, which includes the input text and the URL and headers.
-   The HTTP `POST /v1/synthesize` method accepts a maximum of 8 KB for the URL and headers, and a maximum of 5 KB for the input text that is sent in the body of the request.
-   The WebSocket `/v1/synthesize` method accepts a maximum of 5 KB of input text.

These limits include all characters of the input, including whitespace.

### Language and audio support
{: #features-languages-formats}

The service supports speech synthesis for many languages and audio formats.

-   For information about the supported languages, see [Language support](/docs/text-to-speech-data?topic=text-to-speech-data-about#about-languages).
-   For information about the supported audio formats, see [Audio formats](/docs/text-to-speech-data?topic=text-to-speech-data-about#about-formats).

## Using speech synthesis features
{: #features-synthesis}

The service supports additional features that you can use to tailor the text that you send and the audio that you receive.

### SSML
{: #features-ssml}

You can pass the service plain text or text that is annotated with the Speech Synthesis Markup Language (SSML). SSML is an XML-based markup language that provides annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service.

-   For more information about specifying input text, see [Specifying input text](/docs/text-to-speech-data?topic=text-to-speech-data-usingHTTP#input).
-   For more information about using SSML, see [Using SSML](/docs/text-to-speech-data?topic=text-to-speech-data-ssml).

### Word timings
{: #features-timings}

With the WebSocket interface, you can obtain timing information about the location of words in the audio that the service returns. Timing information is useful for synchronizing the input text and the audio.

You can use the SSML `<mark>` element to identify specific locations, such as word boundaries, in the audio. For languages other than Japanese, you can also request word timing information for all words of the input text. For more information, see [Obtaining word timings](/docs/text-to-speech-data?topic=text-to-speech-data-timing).

## Customizing the service
{: #features-customization}

The service includes a customization interface that you can use to create custom models for use during speech synthesis. A custom model is a dictionary of words and their translations for a specific language. Each word/translation pair in a model tells the service how to pronounce a word when it occurs in input text.

You can use custom models to create application-specific translations for unusual words for which the service's regular pronunciation rules might yield imperfect pronunciations. For example, your application might routinely encounter domain-specific terms, special terms with foreign origins, personal or geographic names, or abbreviations and acronyms. By using customization, you can define translations that tell the service how you want such terms to be pronounced.

You can define the custom entry for a word/translation pair based on other words, or you can create pronunciations based on phoneme symbols in the standard International Phonetic Alphabet (IPA) or the proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). Customization is available for all languages. For more information about customization, see [Understanding customization](/docs/text-to-speech-data?topic=text-to-speech-data-customIntro).

## Leveraging CORS support
{: #features-cors}

The service supports Cross-Origin Resource Sharing (CORS). By using CORS, web pages can request resources directly from a foreign domain. CORS circumvents the same-origin security policy, which otherwise prevents such requests. Because the service supports CORS, a web page can communicate directly with the service without passing the request through the web server that hosts the page.

For instance, a web page that is loaded from a server in {{site.data.keyword.cloud}} can call the customization API directly, bypassing the {{site.data.keyword.cloud_notm}} server. For more information, see [enable-cors.org](https://enable-cors.org/){: external}.

## Using software development kits
{: #features-sdks}

SDKs are available for the {{site.data.keyword.texttospeechshort}} service to simplify the development of speech applications. The SDKs support many popular programming languages and platforms.

-   For a complete list of SDKs and links to the SDKs on GitHub, see [{{site.data.keyword.watson}} SDKs](/docs/text-to-speech-data?topic=watson-using-sdks).
-   For more information about all methods of the SDKs for the {{site.data.keyword.texttospeechshort}} service, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech-data){: external}.
