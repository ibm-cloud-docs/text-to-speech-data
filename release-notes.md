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

# Release notes
{: #release-notes}

The following versions of {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} are available. The information includes new features and changes for each version of the product and any known limitations.
{: shortdesc}

## Known limitations
{: #limitations}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} has the following known limitation:

-   The neural Japanese voice `ja-JP_EmiV3Voice` is not yet available. Support is pending and will be available soon.

### Version 1.0.0 (June 2019)
{: #v100}

The initial release of the service. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} is based on the {{site.data.keyword.texttospeechfull}} service on the public {{site.data.keyword.cloud_notm}}. For more information about the public service, see [About {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} differs from the public {{site.data.keyword.texttospeechshort}} service in the following ways. You might find this information helpful if you are already familiar with the {{site.data.keyword.texttospeechshort}} service on the public {{site.data.keyword.cloud_notm}}.

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} uses access tokens for authentication. For more information, see [Making requests to the service](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) and the [API reference](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   The endpoints for {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} are specific to your {{site.data.keyword.icp4dfull_notm}} cluster. For more information, see [Making requests to the service](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) and the [API reference](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} supports only neural voices. It does not support standard (concatenative) voices. The neural voices do not support the SSML `<express-as>` and `<voice-transformation>` elements.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} does not perform any request logging. You do not need to use the `X-Watson-Learning-Opt-Out` request header.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} does not support Watson tokens. You cannot use the `X-Watson-Authorization-Token` request header to authenticate with the service.
