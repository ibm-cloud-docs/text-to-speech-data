---

copyright:
  years: 2019
lastupdated: "2019-07-30"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# Tutoriel d'initiation
{: #gettingStarted}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} convertit le texte écrit en discours naturel pour offrir des fonctionnalités de synthèse vocale aux applications. Ce tutoriel basé sur curl peut vous aider à utiliser rapidement le service. Les exemples vous montrent comment appeler les méthodes `POST` et `GET /v1/synthesize` du service pour demander un flux audio.
{: shortdesc}

## Avant de commencer
{: #before-you-begin}

Pour pouvoir utiliser {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}, vous devez d'abord effectuer les étapes suivantes. 

1.  Mettre à disposition une instance de {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. Pour plus d'informations sur la mise à disposition, voir [Installation du service](/docs/services/text-to-speech-data?topic=text-to-speech-data-install).
1.  Dans le menu du client Web {{site.data.keyword.icp4dfull_notm}}, choisissez **My Instances**.
1.  Cliquez sur l'instance {{site.data.keyword.texttospeechshort}} pour ouvrir la page de présentation. Copiez les valeurs de données d'identification `{token}` et `{URL}`.

### Utilisation des exemples curl
{: #getting-started-curl}

Ce tutoriel utilise la commande `curl` pour appeler les méthodes de l'interface HTTP du service. Vérifiez que vous disposez de la commande `curl` sur votre système.

1.  Pour tester si `curl` est installé, exécutez la commande suivante en la ligne de commande. Si la ortie de liste la version `curl` qui prend en charge Secure Sockets Layer (SSL), vous êtes fin prêt pour ce tutoriel.

    ```bash
    curl -V
    ```
    {: pre}

1.  Si nécessaire, installez la version de `curl` avec SSL activé pour votre système d'exploitation depuis [curl.haxx.se](https://curl.haxx.se/){: external}.

Omettez les accolades dans les exemples. Ils indiquent des valeurs de variable.
{: tip}

## Etape 1 : Synthétiser du texte en anglais américain
{: #synthesizeEnglish}

Les commandes suivantes utilisent la méthode `POST /v1/synthesize` pour synthétiser l’entrée en anglais américain en fichiers audio dans deux formats différents. Les deux demandes utilisent la voix anglo-américaine par défaut, `en-US_MichaelVoice`.

1.  Exécutez la commande suivante pour synthétiser la chaîne "hello world" et générer un fichier WAV nommé `hello_world.wav`.
    -   Remplacez `{token}` pat le jeton d'accès de votre instance de service.
    -   Remplacez `{url}` par l'URL de votre instance de service.

    *Utilisateurs Windows : * remplacez la barre oblique inversée (``\`) en fin de chaque ligne par un caret (``^`). Vérifiez qu'il n'y a aucun espace de fin.
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"
    ```
    {: pre}

1.  Exécutez la commande suivante pour synthétiser le même texte mais générer un fichier Ogg (format par défaut) nommé `hello_world.ogg`.
    -   Remplacez `{token}` pat le jeton d'accès de votre instance de service.
    -   Remplacez `{url}` par l'URL de votre instance de service.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"
    ```
    {: pre}

Vous pouvez utiliser un navigateur ou d’autres outils pour lire les fichiers audio générés par les exemples. Pour plus d'informations, voir [Lecture d'un fichier audio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats#formatsPlay).
{: note}

## Etape 2 : Synthétiser du texte en espagnol
{: #synthesizeSpanish}

La commande suivante utilise la méthode `GET /v1/synthesize` pour synthétiser l’entrée en espagnol dans un fichier audio.

1.  Exécutez la commande suivante pour synthétiser la chaîne "hola mundo" et générer un fichier WAV nommé `hola_mundo.wav`. Le texte en entrée est codé dans l'URL. La méthode comprend les paramètres de requête `accept` permettant de spécifier le format audio et `voice` indiquant une voix espagnole, `es-ES_EnriqueV3Voice`.
    -   Remplacez `{token}` pat le jeton d'accès de votre instance de service.
    -   Remplacez `{url}` par l'URL de votre instance de service.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

## Etapes suivantes

-   En savoir plus sur l'interface HTTP du service dans [Interface HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP).
-   En savoir plus sur l'interface WebSocket du service dans [Interface WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).
-   Pour plus de détails sur toutes les méthodes des interfaces du service, voir la [référence d'API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
