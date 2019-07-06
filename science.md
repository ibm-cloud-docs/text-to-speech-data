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

# The science behind the service
{: #science}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} relies on neural voice technology to synthesize human-quality speech from input text. The service first analyzes the input text to determine the desired content. It then uses three Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech and encode the resulting audio:
{: shortdesc}

-   Prosody prediction
-   Acoustic feature prediction
-   Neural vocoder

During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. Neural voices produce speech that is crisp and clear, with a very natural-sounding and smooth audio quality.

The DNNs are trained on natural human speech to predict the acoustic features of the audio. This modular approach has the advantage of enabling fast and easy training, as well as independent control of each component. Once the base networks are trained, they can then be adapted to new speaking styles or voices for branding and personalization purposes. For more information about the service's neural voice technology, see the blog post [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}.

The topic of synthesizing text to speech is inherently complex. For more information about the scientific research behind the service's speech technology, see the documents that are listed in [Research references](/docs/services/text-to-speech-data?topic=text-to-speech-data-references). [Kons and others (2019)](/docs/services/text-to-speech-data?topic=text-to-speech-data-references#kons2019) describes the neural voice technology that underlies the service's voices.
