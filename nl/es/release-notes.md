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

# Notas del release
{: #release-notes}

Están disponibles las versiones siguientes de {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}. La información incluye funciones y cambios nuevos para cada versión del producto y para las limitaciones conocidas.
{: shortdesc}

## Limitaciones conocidas
{: #limitations}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} tiene la siguiente limitación conocida:

-   La voz neuronal japonesa `ja-JP_EmiV3Voice` todavía no está disponible. Está pendiente de soporte y pronto estará disponible.

### Versión 1.0.0 (junio de 2019)
{: #v100}

El release inicial del servicio. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} se basa en el servicio {{site.data.keyword.texttospeechfull}} en {{site.data.keyword.cloud_notm}} público. Para obtener más información sobre el servicio público, consulte
[Acerca de {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} difiere del servicio público de {{site.data.keyword.texttospeechshort}} en lo que se indica a continuación. Es posible que encuentre útil esta información si está familiarizado con el servicio de {{site.data.keyword.texttospeechshort}} en {{site.data.keyword.cloud_notm}} público.

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} utiliza señales de acceso para la autenticación. Para obtener más información, consulte [Cómo realizar solicitudes al servicio](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) y la [Consulta de API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   Los puntos finales de {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} son específicos del clúster de {{site.data.keyword.icp4dfull_notm}}. Para obtener más información, consulte [Cómo realizar solicitudes al servicio](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) y la [Consulta de API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} solamente admite voces neuronales. No da soporte a voces estándares (concatenativas). Las voces neuronales no admiten los elementos SSML `<express-as>` y `<voice-transformation>`.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} no efectúa ningún registro de solicitudes. No es necesario que utilice la cabecera de solicitud `X-Watson-Learning-Opt-Out`.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} no da soporte a señales Watson. No puede utilizar la cabecera de solicitud `X-Watson-Authorization-Token` para autenticarse con el servicio.
