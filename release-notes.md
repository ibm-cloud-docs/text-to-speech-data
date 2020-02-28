---

copyright:
  years: 2019, 2020
lastupdated: "2020-02-27"

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

# Release notes
{: #release-notes}

The following versions of {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} are available. The information includes new features and changes for each version of the product and any known limitations.
{: shortdesc}

## Known limitations
{: #limitations}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} has the following known limitation:

-   When you specify the `audio/ogg;codecs=opus` audio format, you can optionally specify a sampling rate other than the default 48,000 Hz. However, while the service accepts `48000`, `24000`, `16000`, `12000`, or `8000` as a valid sampling rate, it currently disregards a specified value and always returns the audio with a sampling rate of 48 kHz.

## Version 1.1.3 (28 February 2020)
{: #v113}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.3 is now available. For more information about installing the new version of the service, see [Installing the Watson Text to Speech add-on](/docs/text-to-speech-data?topic=text-to-speech-data-tts-installing).

## Version 1.1.2 (27 November 2019)
{: #v112}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.2 is now available. For more information about installing the new version of the service, see [Installing the Watson Text to Speech add-on](/docs/text-to-speech-data?topic=text-to-speech-data-tts-installing).

## Version 1.0.1 (30 August 2019)
{: #v101}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.0.1 is now available. The service now works with {{site.data.keyword.icp4dfull_notm}} 2.1.0.1. The release includes the following changes:

-   The service now supports installing {{site.data.keyword.icp4dfull_notm}} with Red Hat OpenShift. For installation instructions, see [Installing Cloud Pak for Data on Red Hat OpenShift](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/openshift.html){: external} and [Installing the Watson Text to Speech add-on](https://www.ibm.com/support/knowledgecenter/en/SSQNUZ_2.1.0/com.ibm.icpdata.doc/watson/speech-to-text-install.html){: external}.
-   The service now offers the neural Japanese voice `ja-JP_EmiV3Voice`. For more information, see [Supported languages and voices](/docs/text-to-speech-data?topic=text-to-speech-data-voices#languageVoices).
-   Federal Information Security Management Act (FISMA) support is now available for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. The service is FISMA High Ready.

## Version 1.0.0 (28 June 2019)
{: #v100}

The initial release of the service. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} is based on the {{site.data.keyword.texttospeechfull}} service on the public {{site.data.keyword.cloud_notm}}. For more information about the public service, see [About {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/text-to-speech?topic=text-to-speech-about#about){: external}.

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} differs from the public {{site.data.keyword.texttospeechshort}} service in the following ways. You might find this information helpful if you are already familiar with the {{site.data.keyword.texttospeechshort}} service on the public {{site.data.keyword.cloud_notm}}.

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} uses access tokens for authentication. For more information, see [Making requests to the service](/docs/text-to-speech-data?topic=text-to-speech-data-making-requests) and the [API reference](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   The endpoints for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} are specific to your {{site.data.keyword.icp4dfull_notm}} cluster. For more information, see [Making requests to the service](/docs/text-to-speech-data?topic=text-to-speech-data-making-requests) and the [API reference](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} supports only neural voices. It does not support standard (concatenative) voices. The neural voices do not support the SSML `<express-as>` and `<voice-transformation>` elements.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} does not perform any request logging. You do not need to use the `X-Watson-Learning-Opt-Out` request header.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} does not support Watson tokens. You cannot use the `X-Watson-Authorization-Token` request header to authenticate with the service.
