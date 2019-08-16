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

# 版本注意事項
{: #release-notes}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 的下列版本可用。該資訊包括產品每個版本的新特性和變更以及所有已知限制。
{: shortdesc}

## 已知限制
{: #limitations}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 的已知限制如下：

-   神經日文語音 `ja-JP_EmiV3Voice` 尚無法使用。支援目前擱置，不久即將可用。


### 1.0.0 版（2019 年 6 月）
{: #v100}

服務的起始版本。{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 是以公用 {{site.data.keyword.cloud_notm}} 上的 {{site.data.keyword.texttospeechfull}} 服務為基礎。如需公用服務的相關資訊，請參閱[關於 {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}。


{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 與公用 {{site.data.keyword.texttospeechshort}} 服務的不同之處在於下列幾方面。如果您已熟悉公用 {{site.data.keyword.cloud_notm}} 上的 {{site.data.keyword.texttospeechshort}} 服務，您可能會發現此資訊很有用。

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 使用存取記號進行鑑別。如需相關資訊，請參閱[向服務提出要求](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests)及 [API 參考資料](https://{DomainName}/apidocs/text-to-speech-data){: external}。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 的端點是 {{site.data.keyword.icp4dfull_notm}} 叢集特定。如需相關資訊，請參閱[向服務提出要求](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests)及 [API 參考資料](https://{DomainName}/apidocs/text-to-speech-data){: external}。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 僅支援神經語音。不支援標準（合成）語音。神經語音不支援 SSML `<express-as>` 和 `<voice-transformation>` 元素。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 不執行任何要求記載。您無需使用 `X-Watson-Learning-Opt-Out` 要求標頭。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 不支援 Watson 記號。無法使用 `X-Watson-Authorization-Token` 要求標頭向服務進行鑑別。
