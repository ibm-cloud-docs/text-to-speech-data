---

copyright:
  years: 2020
lastupdated: "2021-01-13"

keywords: faqs,frequently asked questions,question,Text to Speech

subcollection: text-to-speech-data

---

{:faq: data-hd-content-type='faq'}
{:support: data-reuse='support'}
{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:support: data-reuse='support'}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}

# Usage FAQs
{: #faq-usage}

FAQs for {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} include questions about speech synthesis, supported languages, audio formats, and other topics.
{: shortdesc}

## What languages does the service support?
{: #faq-language-support}
{: faq}
{: support}

The {{site.data.keyword.texttospeechshort}} service supports male and female voices in various spoken languages. Supported languages include Brazilian Portuguese, English (United Kingdom and United States), French, German, Italian, Japanese, and Spanish (multiple dialects). For more information about the available voices for all languages, see [Languages and voices](/docs/text-to-speech-data?topic=text-to-speech-data-voices).

## How does the service synthesize audio?
{: #faq-voices}
{: faq}
{: support}

The {{site.data.keyword.texttospeechshort}} service offers [neural voices](/docs/text-to-speech-data?topic=text-to-speech-data-voices#neuralVoices) for synthesisizing text to speech. The topic of synthesizing text to speech is inherently complex. For more information, see [The science behind the service](/docs/text-to-speech-data?topic=text-to-speech-data-science).

## What are the output audio formats?
{: #faq-audio-types}
{: faq}
{: support}

By default, the {{site.data.keyword.texttospeechshort}} service returns audio in Ogg format with the Opus codec (`audio/ogg;codecs=opus`). The service supports many other audio formats to suit your application needs. For more information, see [Supported audio formats](/docs/text-to-speech-data?topic=text-to-speech-data-audioFormats#formatsSupported).

## How do I convert my text to speech?
{: #faq-convert}
{: faq}
{: support}

To submit text to the service for synthesized audio output, you make an HTTP or WebSocket request. You can use the API directly or use one of the Watson SDKs. [Getting started](/docs/text-to-speech-data?topic=text-to-speech-data-gettingStarted) offers examples of both the HTTP `POST /v1/synthesize` and `GET /v1/synthesize` methods. The [API & SDK reference](/apidocs/text-to-speech-data){: external} shows examples of all interfaces and methods.

There is no graphical user interface for submitting text. See the [Text to Speech demo](https://www.ibm.com/demos/live/tts-demo/self-service/home){: external} to try an example of the service in action. The demo accepts a small amount of your text as input to generate speech with different voices.

## Can I change how the service interprets input text and produces synthesized audio?
{: #faq-change-synthesis}
{: faq}
{: support}

You can use the Speech Synthesis Markup Language (SSML) to control aspects of the synthesis process such as pronunciation, volume, pitch, speed, and other attributes.

-   For general information, see [Using SSML](/docs/text-to-speech-data?topic=text-to-speech-data-ssml).
-   For information about the supported SSML elements, see [SSML elements](/docs/text-to-speech-data?topic=text-to-speech-data-elements).

## What programming languages can I use?
{: #faq-sdks}
{: faq}
{: support}

The service supports SDKs in many popular programming languages and platforms.

-   For more information about the SDKs and links to them on GitHub, see [{{site.data.keyword.watson}} SDKs](/docs/text-to-speech-data?topic=watson-using-sdks).
-   For more information about all methods of the SDKs for the {{site.data.keyword.texttospeechshort}} service, see the [API & SDK reference](/apidocs/text-to-speech-data){: external}.

## What is the maximum amount of text that I can submit for synthesis?
{: #faq-maximum-input}
{: faq}
{: support}

You can submit the following maximum amount of text for a speech synthesis request with each of the service's method:

-   HTTP `GET /v1/synthesize` method - Maximum of 8 KB of total input, which includes the input text, SSML, and the URL and headers.
-   HTTP `POST /v1/synthesize` method - Maximum of 8 KB for the URL and headers. Maximum of 5 KB for the input text, including SSML.
-   WebSocket `/v1/synthesize` method - Maximum of 5 KB of input text, including SSML.

All characters of the input, including whitespace and those that are part of SSML elements, are counted toward the data maximum. For more information, see [Data limits](/docs/text-to-speech-data?topic=text-to-speech-data-service-features#features-data-limits).

## How does customization work?
{: #faq-custom-understand}
{: faq}
{: support}

The customization interface of the {{site.data.keyword.texttospeechshort}} service creates a dictionary of words and their translations for a specific language. This dictionary is referred to as a custom model. For more information, see [Understanding customization](/docs/text-to-speech-data?topic=text-to-speech-data-customIntro).

## How do I create a custom model?
{: #faq-custom-create}
{: faq}

Review the guidelines for working with the customization interface before you begin. Then, see the steps and examples for creating, querying, updating, and deleting custom models in [Creating and managing custom models](/docs/text-to-speech-data?topic=text-to-speech-data-customModels). Also review [Creating and managing custom entries](/docs/text-to-speech-data?topic=text-to-speech-data-customWords) for examples and guidance about adding relevant training data.

## What limits exist for a custom model?
{: #faq-custom-limits}
{: faq}

The following limits apply to all custom models and entries:

-   A custom model can include a maximum of 20,000 custom entries.
-   A word in a custom entry can contain a maximum of 49 characters.
-   A translation in a custom entry can contain a maximum of 499 characters.

For more information, see [Rules for creating custom entries](/docs/text-to-speech-data?topic=text-to-speech-data-rules).
