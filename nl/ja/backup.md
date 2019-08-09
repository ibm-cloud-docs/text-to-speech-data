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

# バックアップとリストア
{: #backup}

潜在的な災害からリカバリーするために、{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} をバックアップして、リストアに備えておく必要があります。サービスの構成、カスタマイズ、使用法を把握しておく必要があります。 また、いつでもサービスのインスタンスを再作成してデータをリストアできるように準備しておく必要があります。
{: shortdesc}

データ損失の可能性のある重大な障害がクラウド・ソリューションで発生した場合は、災害復旧が問題になります。データ損失が発生した場合は、お客様がデータをリストアして、サービス・インスタンスを最新の状態に戻す必要があります。

{{site.data.keyword.texttospeechshort}} サービスについては、クラウドに保管されるのはカスタム音声モデルのデータだけです。災害復旧計画の一環として、カスタム音声モデルの把握、保存、リストアの準備を行ってください。

### カスタム音声モデルのバックアップ
{: #disaster-recovery-backup}

カスタム音声モデルと各モデルのカスタム項目について以下の情報を保存しておいてください。

-   すべてのカスタム音声モデルと各モデルの定義のリスト。 カスタム・モデルに関する情報をリストするには、以下のようにします。
    -   `GET /v1/customizations` メソッドを使用して、すべてのカスタム・モデルに関する情報をリストします。 詳しくは、[すべてのカスタム・モデルの照会](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQueryAll)を参照してください。
    -   `GET /v1/customizations/{customization_id}` メソッドを使用して、指定したカスタム・モデルに関する情報をリストします。 詳しくは、[カスタム・モデルの照会](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQuery)を参照してください。
-   カスタム音声モデルに含まれているすべてのカスタム項目 (単語/トランスレーションのペア) に関する情報。
    -   `GET /v1/customizations/{customization_id}/words` メソッドを使用して、カスタム・モデルに含まれているすべての単語/トランスレーションのペアに関する情報をリストします。 詳しくは、[カスタム・モデルのすべての単語の照会](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsQueryModel)を参照してください。
    -   `GET /v1/customizations/{customization_id}/words/{word}` メソッドを使用して、カスタム・モデルに含まれている指定した単語/トランスレーションのペアに関する情報をリストします。 詳しくは、[カスタム・モデルの単一の単語の照会](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordQueryModel)を参照してください。

この情報を、障害発生時にカスタム音声モデルを再作成できる形式で保存しておくことがベスト・プラクティスです。 カスタム・モデルとカスタム項目に関する情報を積極的に保守し、以下のセクションに記載する呼び出しを事前に準備しておけば、最速のリカバリーが可能になります。

### カスタム音声モデルのリストア
{: #disaster-recovery-restore}

復旧災害が必要な場合は、バックアップ情報を使用して、カスタム音声モデルと各モデルのカスタム項目を再作成できます。

1.  カスタム音声モデルを再作成するには、`POST /v1/customizations` メソッドを使用します。 詳しくは、[カスタム・モデルの作成](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsCreate)を参照してください。
1.  単語/トランスレーションの複数のペアをカスタム音声モデルに追加するには、`POST /v1/customizations/{customization_id}/words` メソッドを使用します。 詳しくは、[カスタム・モデルへの複数の単語の追加](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsAdd)を参照してください。
1.  単語/トランスレーションの 1 つのペアをカスタム音声モデルに追加するには、`POST /v1/customizations/{customization_id}/words/{word}` メソッドを使用します。 詳しくは、[カスタム・モデルへの単一の単語の追加](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordAdd)を参照してください。

すべてのカスタム項目を 1 回で追加することも、グループに分けて追加することも、1 つずつ追加することも可能です。
