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

# 服务背后的科学
{: #science}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 依赖于神经声音技术将输入文本合成为人类品质的语音。神经声音生成的语音既清脆又清晰，具有非常自然且流畅的音频质量。
{: shortdesc}

服务首先会分析输入文本，以确定需要的内容。它使用由决策树组成的声学模型来生成候选单元以供合成。对于要合成的音素序列中的每个音素，模型会将音素放在前后两个音素的上下文中进行考虑。然后，服务会生成一组声学单元，并将评估其适用性。此步骤通过将搜索仅限于满足某些上下文条件的单元，而废弃其他所有单元，从而降低了搜索的复杂性。

然后，服务使用三个深度神经网络 (DNN) 来预测语音的声学（谱）特征，并将生成的音频编码：

-   韵律预测
-   声学特征预测
-   神经声码器

在合成期间，DNN 会预测语音的音高和音位持续时间（韵律）、谱结构和波形。例如，韵律预测模块会根据从输入文本中抽取的语言特征来生成目标值。这些特征包含词性、词重音、词级别突显和位置特征（例如，句子中音节或词的位置）等属性。

DNN 通过自然的人声进行训练，以预测音频的声学特征。此模块化方法的优势是支持快速轻松的训练，以及独立控制每个组件。训练基本网络之后，它们可以针对品牌形象和个性化目的调整为新的说话风格或声音。

有关服务的神经声音技术的更多信息，请参阅

-   博客帖子 [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   研究论文 [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

将文本合成为语音的主题本质上十分复杂。有关服务语音技术背后的科学研究的更多相关信息，请参阅[研究参考资料](/docs/services/text-to-speech-data?topic=text-to-speech-data-references)中列出的文档。
