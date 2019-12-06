---

copyright:
  years: 2019
lastupdated: "2019-12-06"

keywords: text to speech,IBM cloud pak for data,getting started,tutorial,synthesize audio,speech synthesis

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# Getting started with {{site.data.keyword.texttospeechshort}}
{: #gettingStarted}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} converts written text to natural-sounding speech to provide speech-synthesis capabilities for applications. This curl-based tutorial can help you get started quickly with the service. The examples show you how to call the service's `POST` and `GET /v1/synthesize` methods to request an audio stream.
{: shortdesc}

## Before you begin
{: #before-you-begin}

To use {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}, you must first complete the following steps:

1.  Provision an instance of {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. For more information about provisioning, see [Installing the Watson Text to Speech add-on](/docs/services/text-to-speech-data?topic=text-to-speech-data-stt-installing).
1.  From the {{site.data.keyword.icp4dfull_notm}} web client menu, choose **My Instances**.
1.  Click the {{site.data.keyword.texttospeechshort}} instance to open the overview page. Copy the `{token}` and `{URL}` credential values.

### Using the curl examples
{: #getting-started-curl}

This tutorial uses the `curl` command to call methods of the service's HTTP interface. Make sure that you have the `curl` command installed on your system.

1.  To test whether `curl` is installed, run the following command on the command line. If the output lists the `curl` version that supports Secure Sockets Layer (SSL), you are set for the tutorial.

    ```bash
    curl -V
    ```
    {: pre}

1.  If necessary, install the version of `curl` with SSL enabled for your operating system from [curl.haxx.se](https://curl.haxx.se/){: external}.

Omit the braces from the examples. They indicate variable values.
{: tip}

## Step 1: Synthesize text in US English
{: #synthesizeEnglish}

The following commands use the `POST /v1/synthesize` method to synthesize US English input to audio files in two different formats. Both requests use the default US English voice, `en-US_MichaelVoice`.

1.  Issue the following command to synthesize the string "hello world" and produce a WAV file that is named `hello_world.wav`.
    -   Replace `{token}` with the access token for your service instance.
    -   Replace `{url}` with the URL for your service instance.

    *Windows users,* replace the backslash (`\`) at the end of each line with a caret (`^`). Make sure there are no trailing spaces.
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"
    ```
    {: pre}

1.  Issue the following command to synthesize the same text but produce an Ogg file (the default format) that is named `hello_world.ogg`.
    -   Replace `{token}` with the access token for your service instance.
    -   Replace `{url}` with the URL for your service instance.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"
    ```
    {: pre}

You can use a browser or other tools to play the audio files that are produced by the examples. For more information, see [Playing an audio file](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats#formatsPlay).
{: note}

## Step 2: Synthesize text in Spanish
{: #synthesizeSpanish}

The following command uses the `GET /v1/synthesize` method to synthesize Spanish input to an audio file.

1.  Issue the following command to synthesize the string "hola mundo" and produce a WAV file that is named `hola_mundo.wav`. The input text is URL-encoded. The method includes the query parameters `accept` to specify the audio format and `voice` to specify a Spanish voice, `es-ES_EnriqueV3Voice`.
    -   Replace `{token}` with the access token for your service instance.
    -   Replace `{url}` with the URL for your service instance.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

## Next steps

-   Learn more about the service's HTTP interface in [The HTTP interface](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP).
-   Learn about the service's WebSocket interface in [The WebSocket interface](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).
-   Find detailed information about all methods of the service's interfaces in the [API reference](https://{DomainName}/apidocs/text-to-speech-data){: external}.
