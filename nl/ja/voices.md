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

# 言語と音声
{: #voices}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} は、さまざまな言語、音声、方言をサポートしています。このサービスでは、どの言語についても、少なくとも女性の声が 1 種類用意されています。いくつかの言語では、サービスに複数の音声 (男性の声と女性の声を含む) が用意されています。音声ごとに、方言に応じた抑揚とイントネーションが使用されます。
{: shortdesc}

## サポートされる言語と音声
{: #languageVoices}

表 1 には、言語と方言ごとに用意されている音声が、そのタイプと性別と共にリストされています。すべての音声は[ニューラル音声](#neuralVoices)です。(日本語音声のニューラル・バージョンはまだ使用できません)。要求のオプションの `voice` パラメーターの指定を省略した場合、サービスはデフォルトの `en-US_MichaelV3Voice` 音声を使用します。

<table style="width:100%">
  <caption>表 1. サポートされる言語と音声</caption>
  <tr>
    <th style="text-align:left">言語</th>
    <th style="text-align:center">音声</th>
    <th style="text-align:center">性別</th>
  </tr>
  <tr>
    <td style="text-align:left">ブラジル・ポルトガル語</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">カスティリャ・スペイン語</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">フランス語</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">ドイツ語</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
  <tr>
    <td style="text-align:left">イタリア語</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">中南米スペイン語</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">北米スペイン語</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">英国英語</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td style="text-align:left">米国英語</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">女性</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">男性</td>
  </tr>
</table>

`es-LA_SofiaV3Voice` 音声と `es-US_SofiaV3Voice` 音声は本質的には同じ音声です。この 2 つの音声の最も大きな違いは、$ (ドル記号) の解釈方法です。 中南米バージョンでは*ペソ* という語を使用するのに対し、北米バージョンでは*ドル* という語を使用します。 他にもこの 2 つの音声には小さな違いが存在します。
{: note}

### ニューラル音声
{: #neuralVoices}

ニューラル音声テクノロジーは、複数のディープ・ニューラル・ネットワーク (DNN) を使用して、スピーチの音響 (スペクトル) 特性を予測します。DNN は、自然な人間の発話を使用したトレーニングを受けて、予測される音響特性から音声を生成します。合成の際に、DNN はピッチと音素持続時間 (韻律)、スペクトル構造、および発話の波形を予測します。ニューラル音声は、とても自然に聞こえて滑らかな音声品質を持つ、明瞭でクリアな発音を生成します。


サービスのニューラル音声テクノロジーについて詳しくは、以下を参照してください。

-   ブログ投稿 [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   調査記事 [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

### 音声のカスタマイズ
{: #customizeVoice}

テキストから音声合成を行うときには、サービスは言語依存の発音ルールを適用して、各単語の通常のつづりを表音つづりに変換します。 サービスの発音ルールは一般的な単語には十分に機能しますが、外来語、人名、略語、頭文字などの一般的でない単語には十分に機能しないことがあります。

アプリケーションの語彙にそのような単語が含まれている場合は、カスタマイズ・インターフェースを使用して、サービスにどのように単語を発音させるかを指定できます。 詳しくは、[カスタマイズの理解](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro)を参照してください。

カスタム音声モデルは、特定の音声用ではなく、特定の言語用に作成します。そのため、カスタム・モデルは、指定された言語のすべての音声で使用できます。

## 音声の指定
{: #specifyVoice}

HTTP の `GET /v1/synthesize` および `POST /v1/synthesize` メソッドの両方、ならびに WebSocket の `/v1/synthesize` メソッドは、合成音声を指定するオプションの `voice` 照会パラメーターを取ります。 詳しくは、[HTTP インターフェース](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP)および [WebSocket インターフェース](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket)を参照してください。

サービスは、指定された音声に基づいて、入力テキストの言語を認識します。 必ず、入力テキストの言語に一致する音声を指定するようにしてください。 例えば、フランス語音声 (`fr-FR_ReneeV3Voice`) を指定した場合、サービスは、入力テキストがフランス語で記述されているものと想定します。音声の言語で記述されていないテキスト (例えば、フランス語音声用に英語テキスト) を渡した場合、サービスで意味のある結果が生成されないことがあります。

## 使用可能なすべての音声のリスト表示
{: #listVoices}

`GET /v1/voices` メソッドは、使用可能なすべての音声に関する情報をリスト表示します。 このメソッドは引数は取らず、`voices` という JSON 配列を戻します。 この配列には、音声ごとに別のオブジェクトが含まれています。

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaV3Voice",
      "language": "en-US",
      "gender": "female",
      "url": "{url}/v1/voices/en-US_LisaV3Voice",
      "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": false,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

音声オブジェクトのフィールドには、以下の情報が示されています。

-   `name`。音声の識別子 (例えば、`en-US_LisaV3Voice`)。`/v1/synthesize` メソッドの `voice` パラメーターには、この値を指定します。
-   `language`。音声の言語と地域を示します (例えば、`en-US`)。
-   `gender`。音声を `male` または `female` として識別します。
-   `url`。音声の URL を識別します。
-   `description`。音声の要旨を示します。
-   `customizable`。サービスのカスタマイズ・インターフェースを使用して音声をカスタマイズできるかどうかを示すブール値。 (このフィールドの情報は `custom_pronunciation` フィールドと同じですが、後方互換性のために保持されています)。
-   `supported_features`。この音声でサポートされる以下の追加のサービス機能が表されます。
    -   `voice_transformation`。SSML 要素 `<voice-transformation>` を使用して音声を変換できるかどうかを示すブール値。ニューラル音声では音声変換がサポートされていないため、このフィールドは常に `false` です。
    -   `custom_pronunciation`。サービスのカスタマイズ・インターフェースを使用して音声をカスタマイズできるかどうかを示すブール値。

## 特定の音声のリスト表示
{: #listVoice}

`GET /v1/voices/{voice}` メソッドは、特定の音声に関する情報をリスト表示します。 2 つのパラメーターを取ります。

<table>
  <caption>表 2. <code>voices</code> メソッドのパラメーター</caption>
  <tr>
    <th style="text-align:left; width:18%">パラメーター</th>
    <th style="text-align:center; width:12%">タイプ</th>
    <th style="text-align:center; width:12%">データ型</th>
    <th style="text-align:left">説明</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>必須</em></td>
    <td style="text-align:center">Path</td>
    <td style="text-align:center">String</td>
    <td>
      情報を返す音声を指定します。 音声はその名前で指定します (例えば、<code>en-US_LisaV3Voice</code>)。
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>オプション</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      指定した音声の言語に定義されているカスタム音声モデルの
      GUID (Globally Unique Identifier) を指定します。カスタマイズ ID を含める場合は、カスタム・モデルを所有するサービス・インスタンスの資格情報を指定して要求を行う必要があります。</td>
  </tr>
</table>

`customization_id` パラメーターを省略した場合、指定した音声についてこのメソッドから返される JSON 出力は、`GET /v1/voices` メソッドで 1 つの音声について返される情報と同じです。 `customization_id` を指定した場合は、指定したカスタム音声モデルに関する情報を示す `customization` フィールドが出力に含められます。

```javascript
{
  "name": "en-US_LisaV3Voice",
  "language": "en-US",
  "gender": "female",
  "url": "{url}/v1/voices/en-US_LisaV3Voice",
  "description": "Lisa: American English female voice.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": false,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

追加の `customization` フィールドには、カスタム音声モデルの GUID、名前、言語、説明などの情報を示す属性があります。 また、モデルの所有者の資格情報、モデルの作成日時、最終変更日時も表示されます。
