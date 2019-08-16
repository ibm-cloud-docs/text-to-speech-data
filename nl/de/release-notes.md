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

# Releaseinformationen
{: #release-notes}

Die folgenden Versionen von {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} sind verfügbar. Die Informationen enthalten neue Funktionen und Änderungen für jede Version des Produkts sowie alle bekannten Einschränkungen.
{: shortdesc}

## Bekannte Einschränkungen
{: #limitations}

Für {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} gibt es die folgende bekannte Einschränkung:

-   Die neuronale japanische Stimme `ja-JP_EmiV3Voice` ist noch nicht verfügbar. Die Unterstützung hierfür steht künftig bereit und ist in Kürze verfügbar.

### Version 1.0.0 (Juni 2019)
{: #v100}

Das erste Release des Service. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} basiert auf dem {{site.data.keyword.texttospeechfull}}-Service in der öffentlichen {{site.data.keyword.cloud_notm}}. Weitere Informationen zum öffentlichen Service finden Sie in den [Produktinformation zu {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.

Zwischen {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} und dem öffentlichen {{site.data.keyword.texttospeechshort}}-Service gibt es die folgenden Unterschiede. Diese Informationen könnten hilfreich für Sie sein, falls Sie bereits mit dem {{site.data.keyword.texttospeechshort}}-Service in der öffentlichen {{site.data.keyword.cloud_notm}} vertraut sind.

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} verwendet Zugriffstoken für die Authentifizierung. Weitere Informationen finden Sie unter [Anforderungen an den Service ausgeben](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) und in der [API-Referenz](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   Die Endpunkte für {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} gelten speziell für Ihren {{site.data.keyword.icp4dfull_notm}}-Cluster. Weitere Informationen finden Sie unter [Anforderungen an den Service ausgeben](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) und in der [API-Referenz](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} unterstützt nur neuronale Stimmen. Standardstimmen (konkatenative Stimmen) werden nicht unterstützt. Die SSML-Elemente `<express-as>` und `<voice-transformation>` werden von den neuronalen Stimmen nicht unterstützt.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} führt keine Anforderungsprotokollierung durch. Sie müssen den Anforderungsheader `X-Watson-Learning-Opt-Out` nicht verwenden.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} unterstützt keine Watson-Tokens. Die Verwendung des Anforderungsheaders `X-Watson-Authorization-Token` für die Authentifizierung beim Service ist nicht möglich.
