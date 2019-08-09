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

# サービスの背景にある科学
{: #science}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} は、入力テキストから人間のクオリティーの音声を合成するために、ニューラル音声テクノロジーに依存します。ニューラル音声は、とても自然に聞こえて滑らかな音声品質を持つ、明瞭でクリアな発音を生成します。
{: shortdesc}

サービスは最初に、入力テキストを分析して目的のコンテンツを判別します。このサービスは、合成の候補ユニットを生成するデシジョン・ツリーから構成される音響モデルを使用します。合成する音のシーケンスに含まれる 1 音ごとに、モデルは、その音の直前および直後の 2 つの音のコンテキストを考慮します。 その後、適合性が評価される音響ユニットのセットを生成します。このステップで、あるコンテキスト基準を満たすユニットのみに検索を制限し、他のすべてを破棄することによって、検索の複雑さが軽減されます。

その後、サービスは以下の 3 つのディープ・ニューラル・ネットワーク (DNN) を使用して、発話の音響 (スペクトル) 特性を予測し、生成される音声をエンコードします。

-   韻律予測
-   音響特性予測
-   ニューラル・ボコーダー

合成の際に、DNN はピッチと音素持続時間 (韻律)、スペクトル構造、および発話の波形を予測します。例えば、韻律予測モジュールは、入力テキストから抽出される言語特性のターゲット値を生成します。その特性には、品詞、語彙強勢、単語レベルのプロミネンス、位置特性 (例えば、センテンス内の音節または単語の位置) などの属性が含まれます。

DNN は、音声の音響特性を予測できるように、自然な人間のスピーチを使用したトレーニングを受けています。このモジュラー・アプローチには、素早く簡単なトレーニングが可能になり、各コンポーネントを独立して制御できるという利点があります。基本のネットワークがトレーニングを受けた後、ブランディングと個別設定のために、それらを新しい発話スタイルや音声に適応させることができます。

サービスのニューラル音声テクノロジーについて詳しくは、以下を参照してください。

-   ブログ投稿 [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   調査記事 [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

テキストからの音声合成のトピックは本質的に複雑です。サービスのスピーチ・テクノロジーを支えている科学的研究について詳しくは、[研究資料](/docs/services/text-to-speech-data?topic=text-to-speech-data-references)にリストしている資料を参照してください。
