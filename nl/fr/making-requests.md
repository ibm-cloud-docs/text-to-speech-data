---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-27"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Demandes au service
{: #making-requests}

Pour effectuer des demandes au service {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}, vous devez mettre à disposition une instance du service et obtenir des données d'identification. Vous utilisez une URL différente pour les interfaces HTTP et WebSocket du service. Si vous utilisez un certificat autosigné, vous devez désactiver la vérification SSL pour les demandes au service.
{: shortdesc}

## Mise à disposition d'une instance et obtention des données d'identification
{: #making-requests-provisioning}

Avant d'utiliser le service {{site.data.keyword.texttospeechshort}}, vous devez mettre à disposition une instance de ce service et obtenir vos données d'identification. Pour plus d'informations, reportez-vous à la rubrique [Avant de commencer](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin).
A la dernière étape de cette procédure, vous copiez les éléments `{token}` et `{URL}` pour votre instance de service :

-   L'élément `{token}` vous fournit le jeton d'accès pour l'authentification auprès du service. Vous pouvez utiliser le jeton d'accès affiché dans le client Web {{site.data.keyword.icp4dfull_notm}}. Toutefois, dans un environnement de production, utilisez un jeton que vous générez à l'aide d'un programme pour votre instance de service. Pour plus d'informations et pour des exemples, voir *Authentication* dans la [référence d'API](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}.

Pour vous authentifier auprès du service {{site.data.keyword.texttospeechshort}}, vous transmettez votre jeton d'accès avec chaque demande. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} est une solution de cloud à service partagé. Vos données d'identification accordent un accès uniquement à vos données, et celles-ci sont isolées des autres utilisateurs.
-   L'élément `{URL}` fournit le noeud final de base que vous utilisez pour appeler les méthodes du service.

L'URL contient les composants suivants :

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

Les valeurs de variable entre accolades (`{}`) fournissent les informations suivantes :

-   `{icp4d_cluster_host}` est le nom ou l'adresse IP de l'hôte sur lequel votre cluster {{site.data.keyword.icp4dfull_notm}} est déployé. 
-   `{:port}` est le numéro de port sur lequel le service écoute les demandes sur l'hôte spécifié. Vous devez faire précéder le numéro de port par un deux points (`:`).
-   `{release}` est le nom d'édition qui a été indiqué lors de l'installation de la charte Helm.
-   `{instance_id}` est l'identificateur de votre instance de service.

Les accolades indiquent les chaînes de variable que vous devez remplacer par des valeurs littérales. N'incluez pas les accolades dans les appels réels au service.
{: note}

## Création d'une demande HTTP authentifiée
{: #httpRequest}

Le service {{site.data.keyword.texttospeechshort}} propose une [interface HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) qui permet d'accéder à tous les fonctionnalités du service, y compris les interfaces de personnalisation. L'interface HTTP accepte les demandes via le protocole HTTP Secure, lequel repose sur le protocole Secure Sockets Layer (SSL) (ou Transport Layer Security (TLS)). Toutes les URL des demandes adressées à l'interface HTTP commencent par la spécification de protocole `https`. 

Les exemples de la présente documentation utilisent la commande `curl` pour appeler l'interface HTTP du service. Pour plus d'informations, voir [Utilisation des exemples curl](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl). Le format de base d'une demande HTTP avec `curl` inclut les composants suivants :

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

Les valeurs de variable entre accolades fournissent les informations suivantes :

-   `{http_method}` indique la méthode de demande HTTP pour l'exemple : `POST`, `PUT`, `GET` ou `DELETE`. La méthode de demande est requise avec `curl` pour tout autre élément que `GET`.
-   `{token}` fournit le jeton d'accès de votre instance de service. Vous devez utiliser le jeton d'accès pour effectuer une demande sécurisée au service.
-   `{method}` est la méthode du service que vous appelez. Par exemple, vous utilisez la méthode `synthesize` pour effectuer une demande HTTP sur le service.

Les autres valeurs de variable fournissent les informations qui ont été décrites précédemment. De nombreuses méthodes ont des noms plus longs et incluent des paramètres de chemin que vous devez spécifier dans la demande. La plupart des exemples incluent également des en-têtes de requête, des paramètres de requête et d'autres valeurs.

Les exemples illustrent l'URL des appels à l'interface HTTP sous la forme `{url}/v1/{method}`. Remplacez `{url}` par la valeur décrite plus haut.
{: note}

## Création d'une demande WebSocket authentifiée
{: #websocketRequest}

Le service {{site.data.keyword.texttospeechshort}} propose une [interface WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) qui permet une synthèse vocale uniquement. Le service accepte les demandes via le protocole WebSocket Secure, lequel repose sur le protocole Secure Sockets Layer (SSL) (ou Transport Layer Security (TLS)). Toutes les URL des demandes adressées à l'interface WebSocket commencent par la spécification de protocole `wss`. 

Vous pouvez appeler l'interface WebSocket uniquement à partir du code d'application. Vous ne pouvez pas appeler l'interface WebSocket à partir de la ligne de commande. Vous établissez une connexion WebSocket au service sur le noeud final suivant.

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

Les valeurs de variable fournissent les informations qui ont été décrites précédemment. Vous transmettez votre jeton d'accès via le paramètre de requête `access_token` de la méthode.

Les exemples illustrent l'URL des appels à l'interface WebSocket sous la forme `{ws_url}/v1/synthesize`. Remplacez `{ws_url}` par la valeur décrite plus haut.
{: note}

## Désactivation de la vérification SSL
{: #SSLverification}

Tous les services Watson utilisent SSL (ou TLS) pour les connexions et les communications sécurisées entre le client et le serveur. La connexion est vérifiée par rapport au magasin de certificats local pour garantir l'authentification, l'intégrité et la confidentialité.

{{site.data.keyword.icp4dfull_notm}} installe un certificat autosigné. Ce certificat ne peut pas être vérifié par défaut. Vous pouvez effectuer l'une des opérations suivantes pour vous connecter à une instance de service : 

-   Ajouter le certificat autosigné au magasin de clés de confiance de votre agent utilisateur.

    Par exemple, pour effectuer des demandes sécurisées avec `curl`, ajoutez le certificat au magasin de clés de confiance pour `curl`. Pour effectuer des demandes sécurisées à partir de votre navigateur, ajoutez le certificat au magasin de clés de confiance du navigateur.
-   Désactivez la vérification SSL.

    La désactivation de la vérification SSL compromet la sécurité de la connexion et des données. Elle est fortement déconseillée. Désactivez SSL uniquement si cela est absolument nécessaire, et prenez les mesures nécessaires pour activer SSL dès que possible.     {: important}

    -   Pour désactiver la vérification SSL pour une demande `curl`, utilisez l'option `--insecure` (`-k`) avec la demande. Cette option indique à la commande d'ignorer la vérification des certificats SSL de l'outil.
    -   Pour désactiver la vérification SSL pour une demande WebSocket, utilisez l'approche appropriée pour votre bibliothèque client ou utilisez l'un des logiciels SDK {{site.data.keyword.ibmwatson}}{{site.data.keyword.texttospeechshort}}.

Pour plus d'informations sur la désactivation de la vérification SSL pour les appels au service, voir *Disabling SSL verification* dans la [référence d'API](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}. Les informations incluent des exemples pour `curl` et pour tous les logiciels SDK.
