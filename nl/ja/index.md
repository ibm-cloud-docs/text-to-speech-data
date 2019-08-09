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

# 製品情報
{: #about}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} は、記述テキストを自然に聞こえる音声に変換する音声合成機能をアプリケーションに提供します。このサービスでは、遅延を最小限に抑えて、結果がストリーミングでクライアントに戻されます。 このサービスには、[HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) インターフェースと [WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) インターフェースの両方が用意されています。

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} のインストールと構成については、[サービスのインストール](/docs/services/text-to-speech-data?topic=text-to-speech-data-install)を参照してください。

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} は、パブリック {{site.data.keyword.cloud_notm}} 上の {{site.data.keyword.texttospeechfull}} サービスに基づいています。パブリック・サービスについて詳しくは、[{{site.data.keyword.texttospeechshort}} について](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}を参照してください。
{: note}

## 特徴および機能

{{site.data.keyword.texttospeechshort}} サービスには以下の特徴と機能があります。

-   **音声フォーマット** - Opus または Vorbis のコーデックを使用する Ogg または WebM、WAV、FLAC、MP3 (MPEG)、l16 (PCM)、mulaw、基本フォーマットの音声を生成します。 詳しくは、[音声フォーマット](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats)を参照してください。
-   **音声** - テキストからさまざまな言語、音声、方言による出力を合成します。 詳しくは、[言語と音声](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices)を参照してください。
-   **SSML** - プレーン・テキストまたは XML ベースの Speech Synthesis Markup Language (SSML) でマークアップしたテキストを取ります。 詳しくは、[SSML の使用](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml)を参照してください。
-   **単語のタイミング** - WebSocket インターフェースは、SSML の `<mark>` 要素に対応しています。オプションとして、入力テキストのすべてのストリングの単語のタイミング情報も取得できます。 タイミング情報を使用すれば、入力テキストと合成音声を同期することができます。 詳しくは、[単語のタイミングの取得](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing)を参照してください。
-   **カスタマイズ** - カスタマイズ・インターフェースを使用して、入力に含まれている一般的でない単語の発音方法を指定できます。 International Phonetic Alphabet (IPA) または {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) を使用して、発音を定義できます。 詳しくは、[カスタマイズの理解](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro)を参照してください。

## 言語サポート
{: #languages-index}

このサービスは、ブラジル・ポルトガル語、英語 (英国方言と米国方言)、フランス語、ドイツ語、イタリア語、日本語、スペイン語 (カスティリャ方言、中南米方言、北米方言) の音声に対応しています。

このサービスでは、どの言語についても、少なくとも女性の声が 1 種類用意されています。いくつかの言語では、サービスに複数の音声 (男性の声と女性の声を含む) が用意されています。音声ごとに、方言に応じた抑揚とイントネーションが使用されます。

各言語で利用できる音声の詳細については、[言語と音声](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices)を参照してください。

日本語の音声は保留中であり、まもなく使用可能になります。
{: note}

## ユース・ケース
{: #usecases}

このサービスは、画面のない音声主体のアプリケーション (優先される出力方式が音声であるアプリケーション) に適しています。

-   障がい者向けのインターフェース (視覚障がい者向けの支援ツールなど)
-   テキストや E メール・メッセージを作業者に対して読み上げるアプリケーション
-   ビデオ・スクリプトのナレーションやビデオのナレーション
-   読むことが主体の教育ツール
-   ホーム・オートメーション・ソリューション

## このサービスをお試しください

{{site.data.keyword.texttospeechshort}} サービスの実際の例については、以下を参照してください。

-   {{site.data.keyword.texttospeechshort}} サービスの[クイック・デモ](https://text-to-speech-demo.ng.bluemix.net/){: external}。テキストを受け取ってさまざまな種類の音声を生成します。感情表出と変換がサポートされている場合は、その機能も利用できます。
-   {{site.data.keyword.ibmwatson}} [スターター・キット](http://www.ibm.com/watson/developercloud/starter-kits.html){: external}内のアプリケーション。{{site.data.keyword.texttospeechshort}} サービスのデモをします。
