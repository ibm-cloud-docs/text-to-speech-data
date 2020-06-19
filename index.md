---

copyright:
  years: 2019, 2020
lastupdated: "2020-06-16"

subcollection: text-to-speech-data

---

{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}
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

# About
{: #about}

> ** Service update:** *{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} was updated on 19 June 2020. The service now supports five new neural voices. It also includes greatly improved installation, configuration, and backup and restore procedures. For more information, see the [Version 1.1.4 service update](/docs/text-to-speech-data?topic=text-to-speech-data-release-notes#v114) in the release notes.*

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} provides speech synthesis capabilities for your applications to convert written text to natural-sounding speech. The service streams the results back to the client with minimal delay. The service offers both [HTTP](/docs/text-to-speech-data?topic=text-to-speech-data-usingHTTP) and [WebSocket](/docs/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) interfaces.

For information about installing and configuring {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}, see [Installing Watson Text to Speech version 1.1.4](/docs/text-to-speech-data?topic=text-to-speech-data-speech-install).

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} is based on the {{site.data.keyword.texttospeechfull}} service on the public {{site.data.keyword.cloud_notm}}. For more information about the public service, see [About {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/text-to-speech?topic=text-to-speech-about#about){: external}.
{: note}

## Features and capabilities
{: #features-index}

The {{site.data.keyword.texttospeechshort}} service offers the following features and capabilities:

-   **Audio formats** - Produces audio in Ogg or WebM with the Opus or Vorbis codec, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw, or basic format. For more information, see [Audio formats](/docs/text-to-speech-data?topic=text-to-speech-data-audioFormats).
-   **Voices** - Synthesizes text to audio in various languages, voices, and dialects. For more information, see [Languages and voices](/docs/text-to-speech-data?topic=text-to-speech-data-voices).
-   **SSML** - Accepts plain text or text that is marked up with the XML-based Speech Synthesis Markup Language (SSML). For more information, see [Using SSML](/docs/text-to-speech-data?topic=text-to-speech-data-ssml).
-   **Word timings** - With the WebSocket interface, supports the SSML `<mark>` element and optional word timing information for all strings of the input text. Timing information synchronizes the input text and the resulting audio. For more information, see [Obtaining word timings](/docs/text-to-speech-data?topic=text-to-speech-data-timing).
-   **Customization** - Provides a customization interface that you can use to specify how the service pronounces unusual words that occur in your input. You can define pronunciations with the International Phonetic Alphabet (IPA) or {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). For more information, see [Understanding customization](/docs/text-to-speech-data?topic=text-to-speech-data-customIntro).

## Language support
{: #languages-index}
{: help}
{: support}

The service supports voices in the following languages:

-   Brazilian Portuguese
-   English (United Kingdom and United States dialects)
-   French
-   German
-   Italian
-   Japanese
-   Spanish (Castilian, Latin American, and North American dialects)

The service offers at least one female voice for each language. For some languages the service offers multiple voices, including both male and female voices. Each voice uses appropriate cadence and intonation for its dialect.

For more information about the voices that are available for each language, see [Languages and voices](/docs/text-to-speech-data?topic=text-to-speech-data-voices).

## FISMA support
{: #fisma}

Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} offerings purchased on or after August 30, 2019 (version 1.0.1). {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} is FISMA High Ready.

## Use cases
{: #usecases}

The service is appropriate for voice-driven and screenless applications, where audio is the preferred method of output:

-   Interfaces for the disabled, such as assistance tools for the vision-impaired
-   Reading text and email messages aloud to drivers
-   Video-script narration and video voice over
-   Reading-based educational tools
-   Home-automation solutions

## Try out the service

For examples of the {{site.data.keyword.texttospeechshort}} service in action, see

-   A [quick demo](https://text-to-speech-demo.ng.bluemix.net/){: external} of the {{site.data.keyword.texttospeechshort}} service that accepts text and generates speech with different voices. It offers expressiveness and transformation where supported.
-   Applications in {{site.data.keyword.ibmwatson}} [Starter Kits](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} that demonstrate the {{site.data.keyword.texttospeechshort}} service.
