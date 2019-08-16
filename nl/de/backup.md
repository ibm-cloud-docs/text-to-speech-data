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

# Sicherung und Wiederherstellung
{: #backup}

Damit eine Wiederherstellung nach einem Katastrophenfall möglich ist, müssen Sie eine Sicherungskopie von {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} erstellen und die Wiederherstellung des Service vorbereiten. Sie müssen selbst dafür sorgen, dass Sie Ihre Konfiguration, Ihre Anpassung und Ihre Nutzung des Service kennen. Sie sind ebenfalls dafür verantwortlich, alle Vorbereitungen für die erneute Erstellung einer Instanz des Service und für die Wiederherstellung Ihrer Daten zu treffen.
{: shortdesc}

Die Disaster-Recovery kann problematisch sein, falls in Ihrer Cloudlösung ein erheblicher Fehler auftritt, der auch einen möglichen Datenverlust einschließt. Bei einem Datenverlust müssen Sie Ihre Daten wiederherstellen, um die Serviceinstanz wieder in den aktuellen Zustand zu versetzen. 

Beim {{site.data.keyword.texttospeechshort}}-Service werden nur Daten für angepasste Sprechmodelle in der Cloud gespeichert. Für Ihren Disaster-Recovery-Plan müssen Sie auch Ihre angepassten Sprechmodelle kennen, aufbewahren und auf eine Wiederherstellung vorbereiten.

### Angepasste Sprechmodelle sichern
{: #disaster-recovery-backup}

Bewahren Sie die folgenden Informationen zu Ihren angepassten Sprechmodellen und deren angepassten Einträgen auf:

-   Liste aller angepassten Sprechmodelle und ihrer Definitionen. So können Sie Informationen zu Ihren angepassten Modellen auflisten:
    -   Verwenden Sie die Methode `GET /v1/customizations`, um Informationen zu allen angepassten Modellen aufzulisten. Weitere Informationen hierzu finden Sie unter [Alle angepassten Modelle abfragen](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQueryAll).
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}`, um Informationen zu einem angegebenen angepassten Modell aufzulisten. Weitere Informationen hierzu finden Sie unter [Angepasstes Modell abfragen](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsQuery).
-   Informationen zu allen angepassten Einträgen (Paare aus Wort und Umsetzung) in Ihren angepassten Sprechmodellen:
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/words`, um Informationen zu allen Paaren aus Wort und Umsetzung aus einem angepassten Modell aufzulisten. Weitere Informationen hierzu finden Sie unter [Alle Wörter aus einem angepassten Modell abfragen](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsQueryModel).
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/words/{word}`, um Informationen zu einem bestimmten Paar aus Wort und Umsetzung aus einem angepassten Modell aufzulisten. Weitere Informationen hierzu finden Sie unter [Einzelnes Wort aus einem angepassten Modell abfragen](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordQueryModel).

Es hat sich bewährt, diese Informationen in einem Format aufzubewahren, das die erneute Erstellung Ihrer angepassten Sprechmodelle bei einem Fehler möglich macht. Wenn Sie die Informationen zu Ihren angepassten Modellen und angepassten Einträgen aktiv verwalten und im Voraus die im folgenden Abschnitt aufgeführten Aufrufe vorbereiten, können Sie die Wiederherstellung so schnell wie möglich durchführen.

### Angepasste Sprechmodelle wiederherstellen
{: #disaster-recovery-restore}

Falls eine Disaster-Recovery erforderlich werden sollte, können Sie Ihre angepassten Sprechmodelle und deren angepassten Einträge mithilfe der Sicherungsinformationen erneut erstellen:

1.  Verwenden Sie für die erneute Erstellung Ihrer angepassten Sprechmodelle die Methode `POST /v1/customizations`. Weitere Informationen hierzu finden Sie im Abschnitt [Angepasstes Modell erstellen](/docs/services/text-to-speech-data?topic=text-to-speech-data-customModels#cuModelsCreate).
1.  Verwenden Sie zum Hinzufügen mehrerer Paare aus Wort und Umsetzung zu Ihren angepassten Sprechmodellen die Methode `POST /v1/customizations/{customization_id}/words`. Weitere Informationen hierzu finden Sie unter [Mehrere Wörter zu einem angepassten Modell hinzufügen](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsAdd).
1.  Verwenden Sie zum Hinzufügen eines einzelnen Paares aus Wort und Umsetzung zu Ihren angepassten Sprechmodellen die Methode `POST /v1/customizations/{customization_id}/words/{word}`. Weitere Informationen hierzu finden Sie unter [Einzelnes Wort zu einem angepassten Modell hinzufügen](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordAdd).

Alle angepassten Einträge können Sie auf einmal, in Gruppen oder einzeln nacheinander hinzufügen.
