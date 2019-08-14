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

# Disciplines scientifiques sous-jacentes au service
{: #science}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} repose sur la technologie de voix neurale pour synthétiser des paroles humaines à partir de texte d'entrée. Les voix neurales produisent des paroles nettes et claires, avec un son très naturel et une bonne qualité audio.
{: shortdesc}

Le service analyse d'abord le texte d'entrée pour déterminer le contenu souhaité. Il utilise un modèle acoustique composé d'un arbre de décision pour générer des unités candidates pour la synthèse. Pour chacun des téléphones d'une séquence de téléphones à synthétiser, le modèle considère le téléphone dans le contexte des deux téléphones précédent et suivant. Il produit ensuite un ensemble d'unités acoustiques qui sont évaluées pour la forme physique. Cette étape réduit la complexité de la recherche en la limitant aux seules unités répondant à certains critères contextuels et en supprimant toutes les autres. 

Le service utilise ensuite trois réseaux Deep Neural Networks (DNN) pour prévoir les caractéristiques acoustiques (spectrales) du discours et encoder l'audio obtenu :

-   Prévision Prosody
-   Prévision de fonction acoustique
-   Vocoder neural

Au cours de la synthèse, les DNN prévoient le pas et la durée du phonème (prosodie), la structure spectrale et la forme d'onde des paroles. Par exemple, le module Prosody prediction génère des valeurs cible pour les fonctions linguistiques qui sont extraites du texte d'entrée. Cette fonction comprend des attributs tels que partie du discours, accentuation lexicale, importance du mot et caractéristiques de positionnement (place de la syllabe ou du mot dans la phrase). 

Les DNN sont entraînés à partir de paroles humaines naturelles pour prédire les caractéristiques acoustiques de l'audio. Cette approche modulaire a l'avantage de permettre une formation rapide et facile, ainsi que le contrôle indépendant de chaque composant. Une fois les réseaux de base entraînés, ils peuvent être adaptés à de nouveaux styles de langue ou voix à des fins d'image de marque ou de personnalisation. 

Pour plus d'information sur la technologue de voix neurale du service, voir

-   L'article de blogue [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   L'article de recherche [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

Le sujet de la synthèse vocale est par nature complexe. Pour plus d'informations sur la recherche scientifique à l'origine de la technologie de ce service, voir les documents répertoriés dans [Références de recherche](/docs/services/text-to-speech-data?topic=text-to-speech-data-references).
