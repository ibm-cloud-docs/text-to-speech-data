---

copyright:
  years: 2019
lastupdated: "2019-06-22"

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

# Copia de seguridad y restauración
{: #backup}

Para llevar a cabo una recuperación tras posibles desastres, debe realizar una copia de seguridad y estar preparado para restaurar {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}. Usted es responsable de comprender la configuración, personalización y uso del servicio. También es responsable de estar preparado para volver a crear una instancia d
{: shortdesc}

La recuperación tras desastre puede convertirse en un problema si su solución en la nube sufre un fallo significativo que incluye la pérdida potencial de datos. En caso de pérdida de datos, deberá que restaurar los datos para devolver la instancia de servicio a su estado más reciente.

Para el servicio {{site.data.keyword.texttospeechshort}}, sólo se almacenan los datos de los modelos de voz personalizados en la nube. El plan de recuperación tras desastre incluye el conocimiento, la conservación y la preparación para restaurar los modelos de voz personalizados.

### Copia de seguridad de modelos de voz personalizados
{: #disaster-recovery-backup}

Conserve la siguiente información sobre los modelos de voz personalizados y sus entradas personalizadas:

-   Una lista de todos los modelos de voz personalizados y sus definiciones. Para listar la información sobre los modelos personalizados:
    -   Utilice el método `GET /v1/customizations` para listar la información sobre todos los modelos personalizados. Para obtener más información, consulte [Consulta de todos los modelos personalizados](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQueryAll).
    -   Utilice el método `GET /v1/customizations/{customization_id}` para listar información sobre un modelo personalizado especificado. Para obtener más información, consulte [Consulta de un modelo personalizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQuery).
-   Información sobre todas las entradas personalizadas (pares de palabra/conversión) en los modelos de voz personalizados:
    -   Utilice el método `GET /v1/customizations/{customization_id}/words` para listar información sobre todos los pares de palabra/conversión de un modelo personalizado. Para obtener más información, consulte [Consulta de todas las palabras de un modelo personalizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsQueryModel).
    -   Utilice el método `GET /v1/customizations/{customization_id}/words/{word}` para listar información sobre un par de palabra/conversión especificado de un modelo personalizado. Para obtener más información, consulte [Consulta de una palabra de un modelo personalizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordQueryModel).

Una práctica recomendada consiste en conservar esta información en un formato que se puede utilizar para volver a crear los modelos de voz personalizados en caso de que se produzca un error. Realizar de forma activa un mantenimiento de la información sobre los modelos personalizados y las entradas personalizadas, y preparar de forma anticipada las llamadas que se listan en la siguiente sección, puede permitirle recuperar la información lo más rápido posible.

### Restauración de modelos de voz personalizados
{: #disaster-recovery-restore}

Si tiene que recuperarse de un desastre, puede utilizar la información de copia de seguridad para volver a crear los modelos de voz personalizados y sus entradas personalizadas:

1.  Para volver a crear los modelos de voz personalizados, utilice el método `POST /v1/customizations`. Para obtener más información, consulte [Creación de un modelo personalizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsCreate).
1.  Para añadir varios pares de palabra/conversión a los modelos de voz personalizados, utilice el método `POST /v1/customizations/{customization_id}/words`. Para obtener más información, consulte [Añadir varias palabras a un modelo personalizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsAdd).
1.  Para añadir un par de palabra/conversión individuales a los modelos de voz personalizados, utilice el método `POST /v1/customizations/{customization_id}/words/{word}`. Para obtener más información, consulte [Añadir una palabra a un modelo personalizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordAdd).

Puede añadir todas las entradas personalizadas a la vez, en grupos, o de una en una.
