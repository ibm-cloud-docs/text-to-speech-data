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

# Backup e restauração
{: #backup}

Para recuperar-se de potenciais desastres, deve-se fazer backup e estar preparado para restaurar o {{site.data.keyword.texttospeechdatafull}} para o {{site.data.keyword.icp4dfull}}. Você é responsável por entender sua configuração, customização e uso do serviço. Você também é responsável por estar pronto para recriar uma instância do serviço e para restaurar os seus dados.
{: shortdesc}

A recuperação de desastre poderá se tornar um problema se a sua solução de nuvem sofrer uma falha significativa que inclua a potencial perda de dados. No evento de perda de dados, será necessário restaurar os seus dados para retornar a sua instância de serviço para o seu estado mais recente.

Para o serviço do {{site.data.keyword.texttospeechshort}}, apenas os dados para modelos de voz customizados são armazenados na nuvem. Seu plano de recuperação de desastre inclui saber, preservar e estar preparado para restaurar seus modelos de voz customizados.

### Fazendo backup de modelos de voz customizados
{: #disaster-recovery-backup}

Preserve as informações a seguir sobre seus modelos de voz e entradas customizados:

-   Uma lista de todos os seus modelos de voz customizados e suas definições. Para listar informações sobre seus modelos customizados:
    -   Use o método `GET /v1/customizations` para listar informações sobre todos os modelos customizados. Para obter mais informações, consulte [Consultando todos os modelos customizados](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQueryAll).
    -   Use o método `GET /v1/customizations/{customization_id}` para listar informações sobre um modelo customizado especificado. Para obter mais informações, consulte [Consultando um modelo customizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQuery).
-   Informações sobre todas as entradas customizadas (pares de palavra/tradução) em seus modelos de voz customizados:
    -   Use o método `GET /v1/customizations/{customization_id}/words` para listar informações sobre todos os pares de palavra/tradução de um modelo customizado. Para obter mais informações, consulte [Consultando todas as palavras de um modelo customizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsQueryModel).
    -   Use o método `GET /v1/customizations/{customization_id}/words/{word}` para listar informações sobre um par de palavra/tradução especificado de um modelo customizado. Para obter mais informações, consulte [Consultando uma única palavra de um modelo customizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordQueryModel).

Uma melhor prática é preservar essas informações em um formato que possa ser usado para recriar seus modelos de voz customizados no caso de uma falha. Manter ativamente as informações sobre seus modelos e entradas customizados e preparar antecipadamente as chamadas listadas na seção a seguir pode permitir a recuperação o mais rápido possível.

### Restaurando Modelos de Voz Customizados
{: #disaster-recovery-restore}

Se precisar se recuperar de um desastre, será possível usar as informações de backup para recriar seus modelos de voz e entradas customizados:

1.  Para recriar seus modelos de voz customizados, use o método `POST /v1/customizations`. Para obter mais informações, consulte [Criando um modelo customizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsCreate).
1.  Para incluir diversos pares de palavra/tradução em seus modelos de voz customizados, use o método `POST /v1/customizations/{customization_id}/words`. Para obter mais informações, consulte [Incluindo diversas palavras em um modelo customizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsAdd).
1.  Para incluir um par de palavra/tradução único em seus modelos de voz customizados, use o método `POST /v1/customizations/{customization_id}/words/{word}`. Para obter mais informações, consulte [Incluindo uma única palavra em um modelo customizado](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordAdd).

Todas as suas entradas customizadas podem ser incluídas de uma vez, em grupos ou individualmente.
