---

copyright:
  years: 2019
lastupdated: "2019-06-24"

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

# リリース・ノート
{: #release-notes}

使用可能な {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} のバージョンは以下のとおりです。この情報には、製品の各バージョンでの新機能と変更点、および既知の制限事項が含まれています。
{: shortdesc}

## 既知の制限事項
{: #limitations}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} には以下の既知の制限事項があります。

-   ニューラル日本語音声 `ja-JP_EmiV3Voice` はまだ使用できません。サポートは保留中で、少し後に使用可能になります。

### バージョン 1.0.0 (2019 年 6 月)
{: #v100}

サービスの初期リリース。{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} は、パブリック {{site.data.keyword.cloud_notm}} 上の {{site.data.keyword.texttospeechfull}} サービスに基づいています。パブリック・サービスについて詳しくは、[{{site.data.keyword.texttospeechshort}} について](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}を参照してください。


{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} は、以下の点でパブリック {{site.data.keyword.texttospeechshort}} サービスと異なります。パブリック {{site.data.keyword.cloud_notm}} 上の {{site.data.keyword.texttospeechshort}} サービスを既によく知っている場合、この情報が役立つことがあります。

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} は認証のためにアクセス・トークンを使用します。詳しくは、[サービスに対する要求の発行](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests)および [API リファレンス](https://{DomainName}/apidocs/text-to-speech-data){: external}を参照してください。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} のエンドポイントは、使用する {{site.data.keyword.icp4dfull_notm}} クラスターに固有のものです。詳しくは、[サービスに対する要求の発行](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests)および [API リファレンス](https://{DomainName}/apidocs/text-to-speech-data){: external}を参照してください。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} はニューラル音声だけをサポートします。標準 (連結的) 音声はサポートしません。ニューラル音声は、SSML の `<express-as>` 要素や `<voice-transformation>` 要素をサポートしません。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} は要求ロギングを実行しません。`X-Watson-Learning-Opt-Out` 要求ヘッダーを使用する必要はありません。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} は Watson トークンをサポートしません。`X-Watson-Authorization-Token` 要求ヘッダーを使用してサービスを認証することはできません。
