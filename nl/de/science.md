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

# Wissenschaftlicher Hintergrund des Service
{: #science}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} basiert auf der neuronalen Sprachtechnologie, um Sprache in menschlicher Qualität aus Eingabetext zu synthetisieren. Neuronale Stimmen erzeugen Sprache, die klar klingt und eine sehr natürlich klingende und geschmeidige Tonqualität hat.
{: shortdesc}

Der Service analysiert zunächst den Eingabetext, um den gewünschten Inhalt zu bestimmen. Der Service verwendet ein akustisches Modell, das aus einem Entscheidungsbaum besteht, um Kandidateneinheiten für die Synthese zu generieren. Für jeden Laut in einer synthetisch zu erstellenden Lautfolge berücksichtigt das Modell den Laut im Kontext des vorangehenden und des folgenden Lautes. Anschließend erzeugt es eine Reihe von akustischen Einheiten, die hinsichtlich ihrer Eignung ausgewertet werden. Dieser Schritt verringert die Komplexität der Suche, da sie nur auf diejenigen Einheiten beschränkt wird, die einige kontextbezogene Kriterien erfüllen, und alle anderen Einheiten nicht berücksichtigt.

Der Service nutzt dann drei Deep Neural Networks (DNNs), um die akustischen (spektralen) Eigenschaften der Sprache vorherzusagen und die resultierende Audioausgabe zu codieren:

-   Prosodie-Vorhersage
-   Vorhersage für akustische Features
-   Neuronaler Vocodierer

Während der Synthese sagen die DNNs die Tonhöhe und die Phonemdauer (Satzrhythmus), die spektrale Struktur und die Signalform der Sprache voraus. Das Vorhersagemodul 'prosody' generiert beispielsweise Zielwerte für die linguistischen Features, die aus dem Eingabetext extrahiert werden. Zu den Features gehören Attribute wie die Wortart, die lexikalische Betonung, Prominenz auf Wortebene und Positionsmerkmale, z. B. die Position der Silbe oder des Wortes innerhalb des Satzes.

Die DNNs werden auf eine natürliche menschliche Sprache trainiert, um die akustischen Merkmale der Audioausgabe vorherzusagen. Dieser modulare Ansatz hat den Vorteil, ein schnelles und einfaches Training sowie eine unabhängige Steuerung der einzelnen Komponenten zu ermöglichen. Sobald die Basisnetze trainiert sind, können sie dann an neue Sprechstile oder Stimmen für Branding- und Personalisierungszwecke angepasst werden.

Weitere Informationen über die neuronale Sprachtechnologie des Service finden Sie hier:

-   Blogbeitrag [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   Forschungspapier [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

Die synthetische Erstellung von Sprache aus Text ist grundsätzlich komplex. Weitere Informationen zu der wissenschaftlichen Forschung, die hinter der Service-Sprachtechnologie steht, enthalten die Dokumente, die im Abschnitt [Referenzinformationen zur Forschung](/docs/services/text-to-speech-data?topic=text-to-speech-data-references) aufgeführt sind.
