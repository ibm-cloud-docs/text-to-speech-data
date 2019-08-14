---

copyright:
  years: 2019
lastupdated: "2019-07-06"

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

# A propos
{: #about}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} fournit des fonctions de synthèse vocale pour vos applications afin de convertir du texte écrit en paroles. Le service retransmet les résultats au client dans un délai minimal. Le service propose des interfaces [HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) et [WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).

Pour plus d'informations sur l'installation et la configuration de {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}, voir [Installation du service](/docs/services/text-to-speech-data?topic=text-to-speech-data-install).

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} repose sur le service {{site.data.keyword.texttospeechfull}} dans le {{site.data.keyword.cloud_notm}} public. Pour plus d'informations sur le service public, voir [A propos de {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.
{: note}

## Fonctions et capacités

Le service {{site.data.keyword.texttospeechshort}} offre les fonctions et les capacités suivantes :

-   **Formats audio** - Produit un son au format Ogg ou WebM avec les codecs Opus ou Vorbis, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw ou au format de base. Pour plus d'informations, voir [Formats audio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats).
-   **Voix** - Synthétise le texte en audio dans différentes langues, voix et dialectes. Pour plus d'informations, voir [Langues et voix](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).
-   **SSML** - Accepte le texte brut ou le texte marqué avec le langage XML (Speech Synthesis Markup Language). Pour plus d'informations, voir [Utilisation de SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml).
-   **Synchronisation des mots** - Avec l'interface WebSocket, prend en charge l'élément `<mark>` SSML et des informations facultatives de minutage des mots pour toutes les chaînes du texte en entrée. Les informations de minutage permettent de synchroniser le texte d'entrée et l'audio obtenu. Pour plus d'informations, voir [Obtention du minutage des mots](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing).
-   **Personnalisation** - Offre une interface de personnalisation qui vous permet de spécifier la façon dont le service prononce les mots inhabituels qui apparaissent dans votre saisie. Vous pouvez définir des prononciations avec l'alphabet phonétique international (IPA) ou la représentation phonétique symbolique {{site.data.keyword.IBM_notm}} (SPR). Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).

## Support de langue
{: #languages-index}

Le service prend en charge les voix dans les langues suivantes : portugais brésilien, anglais (dialectes britannique et américain), français, allemand, italien, japonais et espagnol (dialectes castillan, latino-américain et nord-américain).

Le service offre au moins une voix féminine pour chaque langue. Pour certaines langues, le service offre plusieurs voix, à la fois masculines et féminines. Chaque voix utilise une cadence et une intonation appropriées pour son dialecte.

Pour plus d'informations sur les voix disponibles pour chaque langue, voir [Langues et voix](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).

Une voix japonaise est en attente et sera bientôt disponible.
{: note}

## Scénarios d'utilisation
{: #usecases}

Ce service convient aux applications vocales et sans écran, où l'audio est la méthode de sortie préférée:

-   Interfaces pour les personnes handicapées, tels que des outils d'assistance pour les malvoyants
-   Lecture de texte et de messages électroniques à voix haute aux conducteurs
-   Narration de scénario vidéo et voix off de vidéo
-   Outils pédagogiques basés sur la lecture
-   Solutions domotiques

## Essayez le service

Pour obtenir des exemples de fonctionnement du service {{site.data.keyword.texttospeechshort}}, voir

-   Une [démonstration rapide](https://text-to-speech-demo.ng.bluemix.net/){: external} du service {{site.data.keyword.texttospeechshort}} qui accepte du texte et génère des paroles dans différentes voix. Il offre les fonctionnalités d'expressivité et de transformation vocale lorsqu'elles sont prises en charge.
-   Des applications dans les [kits de démarrage](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} {{site.data.keyword.ibmwatson}} qui présentent le service {{site.data.keyword.texttospeechshort}}.
