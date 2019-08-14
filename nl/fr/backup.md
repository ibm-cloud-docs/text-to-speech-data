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

# Sauvegarde et restauration
{: #backup}

Pour une reprise après de possibles sinistres, vous devez créer une sauvegarde et être prêt à restaurer {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}. Vous êtes responsable de la compréhension de votre configuration, de la personnalisation et de l'utilisation du service. Vous devez également être prêt à recréer une instance du service et à restaurer vos données.
{: shortdesc}

La reprise après incident peut devenir un problème si votre solution de cloud est confrontée à un échec important incluant la perte potentielle de données. Dans l'éventualité d'une perte de données, vous devez restaurer vos données pour que votre instance de service revienne à son état le plus récent. 

Pour le service {{site.data.keyword.texttospeechshort}}, seules les données des modèles vocaux personnalisés sont stockées dans le cloud. Votre plan de reprise après incident comprend la connaissance, la préservation et la préparation à la restauration de vos modèles vocaux personnalisés.

### Sauvegarde de modèles vocaux personnalisés
{: #disaster-recovery-backup}

Conservez les informations suivantes sur vos modèles vocaux personnalisés et leurs entrées personnalisées :

-   Une liste de tous vos modèles vocaux personnalisés et de leurs définitions. Pour répertorier des informations sur vos modèles personnalisés :
    -   Utilisez la méthode `GET /v1/customizations` pour répertorier des informations sur tous les modèles personnalisés. Pour plus d'informations, voir [Demande de tous les modèles personnalisés](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQueryAll).
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}` pour répertorier des informations sur un modèle personnalisé spécifié. Pour plus d'informations, voir [Demande d'un modèle personnalisé](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQuery).
-   Des informations sur toutes les entrées personnalisées (paires mot/traduction) dans vos modèles vocaux personnalisés :
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/words` pour répertorier des informations sur toutes les paires mot/traduction d'un modèle personnalisé. Pour plus d'informations, voir [Demande de tous les mots d'un modèle personnalisé](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsQueryModel).
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/words/{word}` pour répertorier des informations sur une paire mot/traduction spécifiée à partir d'un modèle personnalisé. Pour plus d'informations, voir [Demande d'un mot à partir d'un modèle personnalisé](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordQueryModel).

Il est recommandé de conserver ces informations dans un format que vous pouvez utiliser pour recréer vos modèles vocaux personnalisés en cas de défaillance. Le fait de conserver activement les informations sur vos modèles et vos entrées personnalisés et de préparer à l'avance les appels répertoriés dans la section suivante peut vous permettre d'effectuer une reprise le plus rapidement possible.

### Restauration de modèles vocaux personnalisés
{: #disaster-recovery-restore}

Si vous devez effectuer une reprise après incident, vous pouvez utiliser les informations de sauvegarde pour recréer vos modèles vocaux personnalisés et leurs entrées personnalisées :

1.  Pour recréer vos modèles vocaux personnalisés, utilisez la méthode `POST /v1/customizations`. Pour plus d'informations, voir [Création d'un modèle personnalisé](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsCreate).
1.  Pour ajouter plusieurs paires mot/traduction à vos modèles vocaux personnalisés, utilisez la méthode `POST /v1/customizations/{customization_id}/words`. Pour plus d'informations, voir [Ajout de plusieurs mots à un modèle personnalisé](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsAdd).
1.  Pour ajouter une paire mot/traduction à vos modèles vocaux personnalisés, utilisez la méthode `POST /v1/customizations/{customization_id}/words/{word}`. Pour plus d'informations, voir [Ajout d'un mot à un modèle personnalisé](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordAdd).

Vous pouvez ajouter toutes vos entrées personnalisées à la fois, groupées, ou une à la fois.
