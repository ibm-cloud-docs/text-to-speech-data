---

copyright:
  years: 2019
lastupdated: "2019-07-08"

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

# 服務背後的科學
{: #science}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 依賴於神經語音技術將輸入文字合成為接近人類的語音。神經語音會產生清脆而清楚的語音，且音訊品質會聽起來很自然平順。
{: shortdesc}

服務首先會分析輸入文字，以確定需要的內容。它使用由決策樹狀結構組成的聲學模型來產生候選單位以供合成。對於要合成之一系列電話中的每通電話，模型會考量前兩通與後兩通電話之上下文中的電話。然後，服務會產生一組聲學單位，並將評估其適用性。此步驟可減少搜尋的複雜性，方法是將其限制為僅限那些符合部分上下文準則的單位，並捨棄所有其他單位。

然後，服務使用三個深度神經網路 (DNN) 來預測語音的聲學（譜）特性，並將產生的音訊編碼：

-   韻律預測
-   聲學特性預測
-   神經聲碼器

在合成期間，DNN 會預測語音的音高和標音持續時間（韻律）、音譜結構和波形。例如，韻律預測模組會根據從輸入文字中擷取的語言特性來產生目標值。這些特性包含詞性、詞彙重音、字級突出處和位置特性（例如，句子中音節或字組的位置）等屬性。

DNN 根據自然人語音進行訓練，以預測音訊的聲學特性。此模組化方法的優勢是可以進行快速輕鬆的訓練，以及獨立控制每個元件。訓練基礎網路之後，它們可以針對品牌行銷和個人化目的調整為新的說話風格或語音。

如需服務神經語音技術的相關資訊，請參閱

-   部落格文章 [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   研究論文 [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

將文字合成為語音的主題本質上十分複雜。如需服務語音技術背後科學研究的相關資訊，請參閱[研究參考資料](/docs/services/text-to-speech-data?topic=text-to-speech-data-references)中列出的文件。
