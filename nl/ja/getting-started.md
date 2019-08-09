---

copyright:
  years: 2019
lastupdated: "2019-07-30"

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

# 入門チュートリアル
{: #gettingStarted}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} は、記述テキストを自然に聞こえる音声に変換して、アプリケーションに音声合成機能を提供します。この curl ベースのチュートリアルを参考にして、このサービスの利用をすぐに開始することができます。 サービスの `POST /v1/synthesize` メソッドと `GET /v1/synthesize` メソッドを呼び出して音声ストリームを要求する方法を、例を通して確認できます。
{: shortdesc}

## 始めに
{: #before-you-begin}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} を使用するには、まず以下のステップを実行する必要があります。

1.  {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} のインスタンスをプロビジョンします。プロビジョニングについて詳しくは、[サービスのインストール](/docs/services/text-to-speech-data?topic=text-to-speech-data-install)を参照してください。
1.  {{site.data.keyword.icp4dfull_notm}} Web クライアントのメニューから、**「マイ・インスタンス (My Instances)」**を選択します。
1.  {{site.data.keyword.texttospeechshort}} インスタンスをクリックすると、概要ページが開きます。 `{token}` と `{URL}` の資格情報値をコピーします。

### curl の使用例
{: #getting-started-curl}

このチュートリアルでは、`curl` コマンドを使用して、サービスの HTTP インターフェースのメソッドを呼び出します。ご使用のシステムに `curl` コマンドがインストールされていることを確認してください。

1.  `curl` がインストールされているかどうかをテストするには、コマンド・ラインで次のコマンドを実行します。Secure Sockets Layer (SSL) をサポートする `curl` のバージョンが出力にリストされたら、チュートリアルの準備ができています。

    ```bash
    curl -V
    ```
    {: pre}

1.  必要であれば、ご使用のオペレーティング・システムに合った SSL 対応バージョンの `curl` を [curl.haxx.se](https://curl.haxx.se/){: external} からインストールします。

例で使用されている中括弧は省略してください。それらは可変値を表しています。
{: tip}

## ステップ 1: 米国英語のテキストの音声合成
{: #synthesizeEnglish}

以下のコマンドでは、`POST /v1/synthesize` メソッドを使用して、米国英語の入力から 2 種類のフォーマットの音声ファイルを合成します。 両方の要求で、デフォルトの米国英語の音声 `en-US_MichaelVoice` を使用します。

1.  以下のコマンドを実行して、「hello world」というストリングから音声を合成して `hello_world.wav` という名前の WAV ファイルを生成します。
    -   `{token}` をサービス・インスタンスのアクセス・トークンに置き換えます。
    -   `{url}` をサービス・インスタンスの URL に置き換えます。

    *Windows ユーザー*: 各行末の円記号 (``\`) をキャレット (``^`) に置き換えます。末尾にスペースがないようにしてください。
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

1.  以下のコマンドを実行して、同じテキストから音声を合成しますが、`hello_world.ogg` という名前の Ogg ファイル (デフォルト・フォーマット) を生成します。
    -   `{token}` をサービス・インスタンスのアクセス・トークンに置き換えます。
    -   `{url}` をサービス・インスタンスの URL に置き換えます。

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"
    ```
    {: pre}

例で生成される音声ファイルは、ブラウザーなどのツールを使用して再生できます。詳しくは、[音声ファイルの再生](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats#formatsPlay)を参照してください。
{: note}

## ステップ 2: スペイン語のテキストの音声合成
{: #synthesizeSpanish}

以下のコマンドでは、`GET /v1/synthesize` メソッドを使用してスペイン語の入力から音声ファイルを合成します。

1.  以下のコマンドを実行して、「hola mundo」というストリングから音声を合成して `hola_mundo.wav` という名前の WAV ファイルを生成します。 入力テキストは URL エンコードします。 このメソッドには、音声フォーマットを指定するための照会パラメーター `accept` と、スペイン語音声 `es-ES_EnriqueV3Voice` を指定するための照会パラメーター `voice` が含まれています。
    -   `{token}` をサービス・インスタンスのアクセス・トークンに置き換えます。
    -   `{url}` をサービス・インスタンスの URL に置き換えます。

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

## 次のステップ

-   サービスの HTTP インターフェースの詳細を [HTTP インターフェース](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP)で確認します。
-   サービスの WebSocket インターフェースの情報を [WebSocket インターフェース](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket)で確認します。
-   サービスのインターフェースのすべてのメソッドに関する詳細情報を [API リファレンス](https://{DomainName}/apidocs/text-to-speech-data){: external}で確認します。
