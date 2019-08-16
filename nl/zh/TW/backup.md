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

# 備份和還原
{: #backup}

若要從可能的災難中回復，必須備份並準備還原 {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}。您負責瞭解服務的配置、自訂作業和使用情形。您也負責準備好以重建服務實例，以及還原資料。
{: shortdesc}

如果您的雲端解決方案遇到包括潛在資料流失的重大失敗，則災難回復可能會變成問題。在資料流失的情況下，您需要還原資料，以將服務實例還原至其最近的狀態。

對於 {{site.data.keyword.texttospeechshort}} 服務，只有自訂語音模型的資料會儲存在雲端中。您的災難回復計劃包括了知道、保留及準備還原自訂語音模型。

### 備份自訂語音模型
{: #disaster-recovery-backup}

保留自訂語音模型及其自訂項目的下列相關資訊：

-   所有自訂語音模型及其定義的清單。若要列出自訂模型的相關資訊，請執行下列動作：
    -   使用 `GET /v1/customizations` 方法，列出所有自訂模型的相關資訊。如需相關資訊，請參閱[查詢所有自訂模型](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQueryAll)。
    -   使用 `GET /v1/customizations/{customization_id}` 方法，列出所指定自訂模型的相關資訊。如需相關資訊，請參閱[查詢自訂模型](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQuery)。
-   自訂語音模型中所有自訂項目（字組/轉換配對）的相關資訊：
    -   使用 `GET /v1/customizations/{customization_id}/cwords` 方法，列出自訂模型中所有字組/轉換配對的相關資訊。如需相關資訊，請參閱[查詢自訂模型中的所有字組](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsQueryModel)。
    -   使用 `GET /v1/customizations/{customization_id}/words/{word}` 方法，列出自訂模型中所指定字組/轉換配對的相關資訊。如需相關資訊，請參閱[查詢自訂模型中的單一字組](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordQueryModel)。

最佳作法是以您可以在失敗時用來重建自訂語音模型的格式保留此資訊。主動維護自訂模型和自訂項目的相關資訊，以及提前準備下節列出的呼叫，可讓您盡快回復。

### 還原自訂語音模型
{: #disaster-recovery-restore}

如果您需要從災難回復，則可以使用備份資訊來重建自訂語音模型及其自訂項目：

1.  若要重建自訂語音模型，請使用 `POST /v1/customizations` 方法。如需相關資訊，請參閱[建立自訂模型](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsCreate)。
1.  若要將多個字組/轉換配對新增至自訂語音模型，請使用 `POST /v1/customizations/{customization_id}/cwords` 方法。如需相關資訊，請參閱[將多個字組新增至自訂模型](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsAdd)。
1.  若要將單一字組/轉換配對新增至自訂語音模型，請使用 `POST /v1/customizations/{customization_id}/words/{word}` 方法。如需相關資訊，請參閱[將單一字組新增至自訂模型](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordAdd)。

您可以一次以群組方式新增所有自訂項目，或一次新增一個。
