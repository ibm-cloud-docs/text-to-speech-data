---

copyright:
  years: 2019, 2020
lastupdated: "2020-10-21"

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

> ** Service update:** *{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} was updated on 19 June 2020. The service now supports five new neural voices, and it includes greatly improved installation, configuration, and backup and restore procedures. **As of 4 September 2020,** the customization interface is generally available; customization is no longer beta functionality. For more information, see the [Version 1.1.4 service update](/docs/text-to-speech-data?topic=text-to-speech-data-release-notes#v114) in the release notes.*

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} provides APIs that use {{site.data.keyword.IBM_notm}}'s speech-synthesis capabilities to convert written text to natural-sounding speech. The service streams the synthesized audio back to the client with minimal delay. The audio uses appropriate cadence and intonation for its language and dialect to provide voices that are smooth and natural.

The service can be used in applications such as voice-automated chatbots, as well as a variety of voice-driven and screenless applications, such as tools for the disabled or visually impaired, video narration and voice over, and educational and home-automation solutions. It is appropriate for any application where audio is the preferred method of output.

For information about installing and configuring {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}, see [Installing {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}} version 1.1.4](/docs/text-to-speech-data?topic=text-to-speech-data-speech-install).

This documentation describes installed instances of {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}. For more information about using a managed instance of {{site.data.keyword.texttospeechshort}} in {{site.data.keyword.cloud_notm}} or in {{site.data.keyword.icp4dfull_notm}} as a Service, see [About {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/text-to-speech?topic=text-to-speech-about#about){: external}.
{: note}

## Speech synthesis
{: #about-synthesis}

The {{site.data.keyword.texttospeechshort}} service supports both HTTP and WebSocket interfaces for speech synthesis. Both interfaces accept plain text and text that is marked up with the XML-based Speech Synthesis Markup Language (SSML). The WebSocket interface can also produce timing information about the words of the audio. For more information, see [Synthesizing speech with the service](/docs/text-to-speech-data?topic=text-to-speech-data-service-features#features-synthesis-interfaces) in the service features.

## Customization
{: #about-customization}

The service provides a customization interface that you can use to specify how the service pronounces unusual words that occur in your input text. You can define custom models to include dictionaries of words for your application's lexicon. For more information, see [Customizing the service](/docs/text-to-speech-data?topic=text-to-speech-data-service-features#features-customization) in the service features.

## Language support
{: #about-languages}
{: help}
{: support}

The service synthesizes text to speech in many languages and dialects:

-   Brazilian Portuguese
-   English (United Kingdom and United States dialects)
-   French
-   German
-   Italian
-   Japanese
-   Spanish (Castilian, Latin American, and North American dialects)

The service offers female and male voices for different languages, and all voices are neural. For more information, see [Languages and voices](/docs/text-to-speech-data?topic=text-to-speech-data-voices).

## Audio formats
{: #about-formats}
{: help}
{: support}

The service produces audio in many popular formats:

-   Ogg or Web Media (WebM) audio with the Opus or Vorbis codec
-   MP3 (or MPEG)
-   Waveform Audio File Format (WAV)
-   Free Lossless Audio Codec (FLAC)
-   Linear 16-bit Pulse-Code Modulation (PCM)
-   Mu-law (or u-law)
-   Basic audio

Different formats support different sampling rates and other characteristics. For more information, see [Audio formats](/docs/text-to-speech-data?topic=text-to-speech-data-audioFormats).

## FISMA support
{: #fisma}

Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} offerings purchased on or after August 30, 2019 (version 1.0.1). {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} is FISMA High Ready.
