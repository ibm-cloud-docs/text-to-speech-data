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

# Notes sur l'édition
{: #release-notes}

Les versions suivantes de {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} sont disponibles. Ces informations incluent les nouvelles fonctionnalités et les modifications de chaque version du produit et les éventuelles limitations connues.
{: shortdesc}

## Limitations connues
{: #limitations}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} présente la limitation connue suivante : 

-   La voix neurale japonais `ja-JP_EmiV3Voice` n'est pas encore disponible. Une prise en charge est en attente et sera bientôt disponible.


### Version 1.0.0 (juin 2019)
{: #v100}

Edition initiale du service. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} repose sur le service {{site.data.keyword.texttospeechfull}} dans {{site.data.keyword.cloud_notm}} public. Pour plus d'informations sur le service public, voir [A propos de {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.


{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} diffère du service {{site.data.keyword.texttospeechshort}} service de plusieurs manières. Ces informations peuvent vous être utiles si vous connaissez déjà le service {{site.data.keyword.texttospeechshort}} dans {{site.data.keyword.cloud_notm}} public.

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} utilise des jetons d'accès pour l'authentification. Pour plus d'informations, voir [Demandes au service](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) et [référence d'API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   Les noeuds finaux de {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} sont spécifiques à votre cluster {{site.data.keyword.icp4dfull_notm}}. Pour plus d'informations, voir [Demandes au service](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) et [référence d'API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} prend uniquement en charge les voix neurales. Il ne prend pas en charge les voix standard (concaténatives). Les voix neurales ne prennent pas en charge les éléments SSML `<express-as>` et `<voice-transformation>`.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} n'effectue aucune consignation de demande. Vous n'avez pas besoin d'utiliser l'en-tête de demande `X-Watson-Learning-Opt-Out`.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} ne prend pas en charge les jetons Watson. Vous ne pouvez pas utiliser l'en-tête de demande `X-Watson-Authorization-Token` pour l'authentification auprès du service.
