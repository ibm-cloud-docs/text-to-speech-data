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

# 备份和复原
{: #backup}

要从可能的灾难中恢复，必须备份并准备复原 {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}。了解服务的配置、定制和使用情况是您的责任。您还应负责准备好重新创建服务实例并复原数据。
{: shortdesc}

如果云解决方案体验遇到重大故障，包括潜在的数据丢失，那么灾难恢复可能会成为问题。在数据丢失的情况下，您需要复原数据，以将服务实例恢复为其最新状态。

对于 {{site.data.keyword.texttospeechshort}} 服务，只有定制声音模型的数据会存储在云中。因此，您的灾难恢复计划应包括了解和保留定制声音模型的相关信息，并准备好复原定制声音模型。

### 备份定制声音模型
{: #disaster-recovery-backup}

保留有关定制声音模型及其定制条目的以下信息：

-   所有定制声音模型及其定义的列表。要列出有关定制模型的信息：
    -   使用 `GET /v1/customizations` 方法可列出有关所有定制模型的信息。有关更多信息，请参阅[查询所有定制模型](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQueryAll)。
    -   使用 `GET /v1/customizations/{customization_id}` 方法可列出有关指定定制模型的信息。有关更多信息，请参阅[查询定制模型](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQuery)。
-   有关定制声音模型中所有定制条目（词/转换项对）的信息：
    -   使用 `GET /v1/customizations/{customization_id}/words` 方法可列出有关定制模型中所有词/转换项对的信息。有关更多信息，请参阅[查询定制模型中的所有词](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsQueryModel)。
    -   使用 `GET /v1/customizations/{customization_id}/words/{word}` 方法可列出有关定制模型中指定词/转换项对的信息。有关更多信息，请参阅[查询定制模型中的单个词](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordQueryModel)。

保留这些信息时，最好采用在发生故障时可以用于重新创建定制声音模型的格式。主动维护有关定制模型和定制条目的信息，并提前准备以下部分中列出的调用，能使您尽快实现恢复。

### 复原定制声音模型
{: #disaster-recovery-restore}

如果需要从灾难恢复，您可以使用备份信息来重新创建定制声音模型及其定制条目：

1.  要重新创建定制声音模型，请使用 `POST /v1/customizations` 方法。有关更多信息，请参阅[创建定制模型](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsCreate)。
1.  要向定制声音模型添加多个词/转换项对，请使用 `POST /v1/customizations/{customization_id}/words` 方法。有关更多信息，请参阅[向定制模型添加多个词](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsAdd)。
1.  要向定制声音模型添加单个词/转换项对，请使用 `POST /v1/customizations/{customization_id}/words/{word}` 方法。 有关更多信息，请参阅[向定制模型添加单个词](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordAdd)。

您可以一次性添加所有定制条目，也可以分组添加定制条目，或一次添加一个定制条目。
