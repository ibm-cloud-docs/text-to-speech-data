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

# 開発者向けの概要
{: #overview}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} の機能は、HTTP Representational State Transfer (REST) API または WebSocket インターフェースを介して利用できます。多様なプログラミング言語でアプリケーション開発を簡単に行えるように、複数の SDK も用意されています。以下のセクションでは、このサービスを使用するアプリケーションの開発の概要を説明します。
{: shortdesc}

要求ごとにアクセス・トークンを渡すことによって、{{site.data.keyword.texttospeechshort}} に対して認証が行われます。{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} はマルチテナント・クラウド・ソリューションです。資格情報によって自身のデータに対するアクセス権限のみが付与され、自身のデータは他のユーザーから分離されています。

## HTTP インターフェース
{: #overview-http}

HTTP API を使用してテキストの音声合成を行うには、サービスの `GET` または `POST` バージョンの `/v1/synthesize` メソッドを呼び出します。 メソッドの 2 つのバージョンは、概して、同等の機能を備えています。

-   *入力テキスト:* 合成する入力テキストは、以下の 2 とおりの方法で渡します。
    -   `GET /v1/synthesize` メソッドは、入力テキストを照会パラメーターで受け取ります。 要求の最大サイズは 8 KB です。これには、入力テキスト、URL、ヘッダーが含まれます。
    -   `POST /v1/synthesize` メソッドは、入力テキストを要求本体の中で受け取ります。 要求の最大サイズは、URL とヘッダーが 8 KB、要求本体で送信する入力テキストが 5 KB です。

    サービスには、プレーン・テキストまたは SSML (Speech Synthesis Markup Language) でアノテーションが付けられたテキストを渡すことができます。 SSML は、{{site.data.keyword.texttospeechshort}} サービスなどの音声合成アプリケーション用のテキストのアノテーションを記述するための XML ベースのマークアップ言語です。

詳しくは、[入力テキストの指定](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP#input)を参照してください。
-   *音声:* サービスはテキストを受け取り、さまざまな言語、音声、方言で出力を生成します。 このサービスでは、どの言語についても、少なくとも女性の声が 1 種類用意されています。言語によっては、サービスは複数の音声を提供しており、男性音声と女性音声の両方が含まれる場合もあります。サービスは、米国英語と英国英語など、異なる方言も提供します。

    サービスの `GET /v1/voices` メソッドまたは `GET /v1/voices/{voice}` メソッドを使用して、サポートされる音声に関する詳細を取得できます。 サービスは、テキストから、指定された音声の言語を合成できます。 必ず、音声と入力テキストを一致させてください。

    詳しくは、[言語と音声](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices)を参照してください。
-   *音声フォーマット:* サービスが生成できる音声のフォーマットは次のとおりです。Opus (デフォルト) または Vorbis コーデックを使用したOgg または Web メディア (WebM) フォーマット、MP3 (Motion Picture Experts Group、つまり MPEG) フォーマット、Waveform Audio ファイル・フォーマット (WAV)、Free Lossless Audio Codec (FLAC)、16 ビットのリニア Pulse-Code Modulation (PCM)、8 ビットの mu-law (u-law)、または基本音声。

    詳しくは、[音声フォーマット](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats)を参照してください。

## WebSocket インターフェース
{: #overview-websocket}

サービスには、テキストからの音声合成に使用できる WebSocket インターフェースが用意されています。 このインターフェースは、最大 5 KB の入力テキストを受け取る単一バージョンの `/v1/synthesize` メソッドを備えています。 合成するテキスト、使用する音声、および音声のフォーマットを指定します。 プレーン・テキスト、または SSML でアノテーションが付けられたテキストを指定できます。 詳しくは、[WebSocket インターフェース](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket)を参照してください。

WebSocket インターフェースは、音声の中の特定の位置を識別する SSML 要素 `<mark>` の使用をサポートしています。 また、入力テキストのすべての単語のタイミング情報を要求することもできます。 詳しくは、[単語のタイミングの取得](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing)を参照してください。

## カスタマイズ・インターフェース
{: #overview-customization}

サービスは、音声合成時に使用するカスタム音声モデルを作成するために使用できるカスタマイズ・インターフェースを備えています。 カスタム音声モデルは、特定の言語の単語とそのトランスレーションから成る辞書です。 モデル内の各単語とトランスレーションのペアは、その単語が入力テキストに含まれていた場合の発音方法をサービスに指示します。

カスタム音声モデルを使用すると、サービスの標準の発音ルールでは適切な発音が生成されない非一般的な単語に対して、アプリケーション固有のトランスレーションを作成できます。 単語/トランスレーションのペアを表すカスタム項目を定義するときには、標準的な International Phonetic Alphabet (IPA) 表記または {{site.data.keyword.IBM_notm}} 専有の Symbolic Phonetic Representation (SPR) を使用できます。

例えば、ご使用のアプリケーションで、特殊な外来語、人名や地名、略語、頭字語が日常的に出現する場合があります。 カスタマイズを使用すれば、そのような用語をどのように発音すればよいのかをサービスに指示するトランスレーションを定義できます。 詳しくは、[カスタマイズの理解](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro)を参照してください。

カスタマイズ・インターフェースはベータ・リリースです。
{: note}

## CORS サポート
{: #cors}

サービスは、Cross-Origin Resource Sharing (CORS) をサポートしています。 CORS を使用すると、Web ページから外部ドメインにあるリソースを直接要求できるようになります。 CORS は、そうした要求を禁止する同一生成元セキュリティー・ポリシーを回避できます。 サービスが CORS をサポートしているため、Web ページは、そのページをホストする Web サーバーを介して要求を渡さずに、サービスと直接通信できます。

例えば、{{site.data.keyword.cloud}} 内のサーバーからロードされた Web ページで、{{site.data.keyword.cloud_notm}} サーバーをバイパスして、カスタマイズ API を直接呼び出すことができます。 詳しくは、[enable-cors.org](https://enable-cors.org/){: external} を参照してください。

## Software Development Kit の使用
{: #sdks}

SDK を使用すれば、{{site.data.keyword.texttospeechshort}} サービスで音声アプリケーションを簡単に開発できます。 一般的なプログラミング言語やプラットフォーム用の {{site.data.keyword.ibmwatson}} SDK がいくつも用意されています。

-   SDK の一覧および GitHub 上の各 SDK へのリンクについては、[SDK の使用](/docs/services/watson?topic=watson-using-sdks)を参照してください。
-   {{site.data.keyword.texttospeechshort}} サービスで使用できる Node、Java&trade;、Python、Ruby、および Go SDK のすべてのメソッドについて詳しくは、[API リファレンス](https://{DomainName}/apidocs/text-to-speech-data){: external}を参照してください。
