---

copyright:
  years: 2019, 2020
lastupdated: "2020-07-06"

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

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} relies on neural voice technology to synthesize human-quality speech from input text. Neural voices produce speech that is crisp and clear, with a very natural-sounding and smooth audio quality.
{: shortdesc}

The service first analyzes the input text to determine the desired content. It uses an acoustic model that consists of a decision tree to generate candidate units for synthesis. For each of the phones in a sequence of phones to be synthesized, the model considers the phone in the context of the preceding and following two phones. It then produces a set of acoustic units that are evaluated for fitness. This step reduces the complexity of the search by restricting it to only those units that meet some contextual criteria and discarding all others.

The service then uses three Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech and encode the resulting audio:

-   Prosody prediction
-   Acoustic feature prediction
-   Neural vocoder

During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. For example, the prosody prediction module generates target values for the linguistic features that are extracted from the input text. The features include such attributes as part of speech, lexical stress, word-level prominence, and positional features such as the position of the syllable or word in the sentence.

The DNNs are trained on natural human speech to predict the acoustic features of the audio. This modular approach has the advantage of enabling fast and easy training, as well as independent control of each component. Once the base networks are trained, they can then be adapted to new speaking styles or voices for branding and personalization purposes.

For more information about the service's neural voice technology, see

-   The blog post [{{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.texttospeechshort}}: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   The research paper [High quality, lightweight and adaptable {{site.data.keyword.texttospeechshort}} using LPCNet](https://arxiv.org/abs/1905.00590){: external}

The topic of synthesizing text to speech is inherently complex. For more information about the scientific research behind the service's speech technology, see the documents that are listed in [Research references](/docs/text-to-speech-data?topic=text-to-speech-data-references).
