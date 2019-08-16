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

# Anforderungen an den Service senden
{: #making-requests}

Wenn Sie authentifizierte Anforderungen an {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} senden möchten, müssen Sie eine Instanz des Service bereitstellen und Berechtigungsnachweise abrufen. Für die HTTP- und WebSocket-Schnittstellen des Service verwenden Sie jeweils eine andere URL. Wenn Sie ein selbst signiertes Zertifikat verwenden, müssen Sie die SSL-Verifizierung für Anforderungen an den Service inaktivieren.
{: shortdesc}

## Instanz bereitstellen und Berechtigungsnachweise abrufen
{: #making-requests-provisioning}

Vor der Verwendung des {{site.data.keyword.texttospeechshort}}-Service müssen Sie eine Instanz des Service bereitstellen und Berechtigungsnachweise abrufen. Weitere Informationen finden Sie in [Vorbereitung](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin). Im letzten Schritt dieser Prozedur kopieren Sie `{token}` und `{URL}` für Ihre Serviceinstanz: 

-   Mit `{token}` wird Ihr Zugriffstoken für die Authentifizierung beim Service angegeben. Sie können das Zugriffstoken verwenden, das im Web-Client von {{site.data.keyword.icp4dfull_notm}} angezeigt wird. In einer Produktionsumgebung müssen Sie jedoch ein Token verwenden, das programmgesteuert für die Serviceinstanz generiert wird. Weitere Informationen und Beispiele finden Sie im Abschnitt *Authentifizierung* in der [API-Referenz](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}.

    Für die Authentifizierung beim {{site.data.keyword.texttospeechshort}}-Service übergeben Sie mit jeder Anforderung Ihr Zugriffstoken. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} ist eine Multi-Tenant-Cloudlösung. Mit Ihren Berechtigungsnachweisen ist nur Zugriff auf Ihre Daten möglich und Ihre Daten werden von anderen Benutzern isoliert.
-   Mit `{URL}` wird der Basisendpunkt angegeben, den Sie zum Aufrufen der Methoden des Service verwenden.

Die URL enthält die folgenden Komponenten:

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

Die Variablenwerte in geschweiften Klammern (`{}`) geben Folgendes an:

-   `{icp4d_cluster_host}` ist der Name oder die IP-Adresse des Hosts, auf dem Ihr {{site.data.keyword.icp4dfull_notm}}-Cluster bereitgestellt ist.
-   `{:port}` ist die Portnummer, an der der Service für Anforderungen auf dem angegebenen Host empfangsbereit ist. Sie müssen der Portnummer einen Doppelpunkt (`:`) voranstellen.
-   `{release}` ist der Releasename, der bei der Installation des Helm-Diagramms angegeben wurde.
-   `{instance_id}` ist die ID Ihrer Serviceinstanz. 

Die geschweiften Klammern geben Variablenzeichenfolgen an, die Sie durch tatsächliche Werte ersetzen müssen. Geben Sie die geschweiften Klammern nicht in den tatsächlichen Aufrufen an den Service an.
{: note}

## Authentifizierte HTTP-Anforderung senden
{: #httpRequest}

Der {{site.data.keyword.texttospeechshort}}-Service bietet eine [HTTP-Schnittstelle](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP), die den Zugriff auf alle Funktionen des Service ermöglicht, einschließlich Anpassungsschnittstellen. Die HTTP-Schnittstelle akzeptiert Anforderungen über das HTTPS-Protokoll, das wiederum auf das SSL-Protokoll (Secure Sockets Layer) oder das TLS-Protokoll (Transport Layer Security) zurückgreift. Alle URLs für Anforderungen an die HTTP-Schnittstelle beginnen mit der Protokollspezifikation `https`.

In den Beispielen dieser Dokumentation wird die HTTP-Schnittstelle des Service mit dem Befehl `curl` aufgerufen. Weitere Informationen finden Sie unter [curl-Beispiele verwenden](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl). Das Basisformat einer HTTP-Anforderung mit `curl` besteht aus den folgenden Komponenten:

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

Die Variablenwerte in geschweiften Klammern geben Folgendes an:

-   `{http_method}` gibt die HTTP-Anforderungsmethode für das Beispiel an: `POST`, `PUT`, `GET` oder `DELETE`. Mit Ausnahme von `GET` ist die Anforderungsmethode bei `curl` erforderlich.
-   `{token}` gibt das Zugriffstoken für Ihre Serviceinstanz an. Sie müssen das Zugriffstoken verwenden, um eine sichere Anforderung an den Service auszugeben.
-   `{method}` ist die Methode des Service, die Sie aufrufen wollen. Zum Beispiel verwenden Sie die Methode `synthesize`, um eine HTTP-Anforderung an den Service auszugeben.

Die übrigen Variablenwerte geben die Informationen an, die bereits beschrieben wurden. Viele Methoden haben längere Namen und enthalten Pfadparameter, die Sie in der Anforderung angeben müssen. Die meisten Beispiele enthalten darüber hinaus auch Anforderungsheader, Abfrageparameter und andere Werte.

In den Beispielen wird die URL für Aufrufe an die HTTP-Schnittstelle als `{url}/v1/{method}` dargestellt. Ersetzen Sie `{url}` durch die oben beschriebenen Werte.
{: note}

## Authentifizierte WebSocket-Anforderung senden
{: #websocketRequest}

Der {{site.data.keyword.texttospeechshort}}-Service bietet eine [WebSocket-Schnittstelle](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket), die nur Sprachsynthese bereitstellt. Der Service akzeptiert Anforderungen über das WSS-Protokoll (WebSocket Secure), das wiederum auf das SSL-Protokoll (Secure Sockets Layer) oder das TLS-Protokoll (Transport Layer Security) zurückgreift. Alle URLs für Anforderungen an eine WebSocket-Schnittstelle beginnen mit der Protokollspezifikation `wss`.

Sie können die WebSocket-Schnittstelle nur über den Anwendungscode aufrufen. Sie können die WebSocket-Schnittstelle nicht über die Befehlszeile aufrufen. Sie erstellen eine WebSocket-Verbindung zum Service an dem folgenden Endpunkt.

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

Die Variablenwerte geben die Informationen an, die bereits beschrieben wurden. Sie übergeben Ihr Zugriffstoken über den Abfrageparameter `access_token` der Methode.

In den Beispielen wird die URL für Aufrufe an die WebSocket-Schnittstelle als `{ws_url}/v1/synthesize` dargestellt. Ersetzen Sie `{ws_url}` durch die oben beschriebenen Werte.
{: note}

## SSL-Verifizierung inaktivieren
{: #SSLverification}

Bei allen Watson-Services wird SSL (oder TLS) für sichere Verbindungen und sichere Kommunikation zwischen dem Client und dem Server verwendet. Die Verifizierung der Verbindung erfolgt mithilfe des lokalen Zertifikatsspeichers, um die Authentifizierung, Integrität und Vertraulichkeit zu gewährleisten. 

{{site.data.keyword.icp4dfull_notm}} installiert ein selbst signiertes Zertifikat. Eine erfolgreiche Verifizierung dieses Zertifikats ist nicht ohne Weiteres möglich. Sie können einen der folgenden Schritte ausführen, damit eine Verbindung zu einer Serviceinstanz erfolgreich hergestellt werden kann:

-   Fügen Sie das selbst signierte Zertifikat dem Truststore für Ihren Benutzeragenten hinzu.

    Sollen beispielsweise sichere Anforderungen mit `curl` ausgegeben werden, fügen Sie das Zertifikat dem Truststore für `curl` hinzu. Sollen sichere Anforderungen über Ihren Browser ausgegeben werden, fügen Sie das Zertifikat dem Truststore für den Browser hinzu.
-   Inaktivieren Sie die SSL-Verifizierung.

    Durch die Inaktivierung der SSL-Verifizierung wird die Sicherheit der Verbindung und der Daten beeinträchtigt. Es wird ausdrücklich davon abgeraten. SSL darf nur inaktiviert werden, wenn dies unbedingt erforderlich ist. Ergreifen Sie in diesem Fall Maßnahmen, um SSL so bald wie möglich wieder zu aktivieren.
    {: important}

    -   Zur Inaktivierung der SSL-Verifizierung für eine `curl`-Anforderung verwenden Sie die Option `--insecure` (`-k`) in der Anforderung. Diese Option bewirkt, dass der Befehl die Verifizierung von SSL-Zertifikaten durch das Tool umgeht.
    -   Zur Inaktivierung der SSL-Verifizierung für eine  WebSocket-Anforderung verwenden Sie die entsprechende Methode für Ihre Clientbibliothek oder eines der {{site.data.keyword.ibmwatson}} {{site.data.keyword.texttospeechshort}}-SDKs.

Weitere Informationen zur Inaktivierung der SSL-Verifizierung für Aufrufe des Service finden Sie in dem Abschnitt über die *Inaktivierung der SSL-Verifizierung* in der [API-Referenz](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}. Die Informationen enthalten Beispiele für `curl` und für alle SDKs.
