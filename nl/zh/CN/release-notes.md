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

# 发行说明
{: #release-notes}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 的下列版本可用。该信息包括产品每个版本的新功能和更改以及所有已知限制。
{: shortdesc}

## 已知限制
{: #limitations}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 的已知限制如下：

-   神经日语声音 `ja-JP_EmiV3Voice` 尚未可用。支持目前暂挂，不久即将可用。


### V1.0.0（2019 年 6 月）
{: #v100}

服务的初始发行版。{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 基于公共 {{site.data.keyword.cloud_notm}} 上的 {{site.data.keyword.texttospeechfull}} 服务。有关公共服务的更多信息，请参阅[关于 {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}。


{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 与公共 {{site.data.keyword.texttospeechshort}} 服务的不同之处在于以下几方面。如果您已熟悉公共 {{site.data.keyword.cloud_notm}} 上的 {{site.data.keyword.texttospeechshort}} 服务，您可能会发现此信息很有用。

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 使用访问令牌进行认证。有关更多信息，请参阅[向服务发出请求](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests)以及 [API 参考](https://{DomainName}/apidocs/text-to-speech-data){: external}。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 的端点是特定于 {{site.data.keyword.icp4dfull_notm}} 集群的。有关更多信息，请参阅[向服务发出请求](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests)以及 [API 参考](https://{DomainName}/apidocs/text-to-speech-data){: external}。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 仅支持神经声音。不支持标准（合成）声音。神经声音不支持 SSML `<express-as>` 和 `<voice-transformation>` 元素。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 不执行任何请求日志记录。您无需使用 `X-Watson-Learning-Opt-Out` 请求头。
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 不支持 Watson 令牌。无法使用 `X-Watson-Authorization-Token` 请求头向服务进行认证。
