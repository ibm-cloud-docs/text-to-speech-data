---

copyright:
  years: 2019
lastupdated: "2019-06-27"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Cluster verwalten
{: #manage}

Nach der Installation und Konfiguration von {{site.data.keyword.texttospeechdatafull}} in {{site.data.keyword.icp4dfull}} können Sie die Instanz und den Cluster verwalten.

## Lokale Maschine vorbereiten
{: #manage-prep-local-machine}

Stellen Sie sicher, dass folgende Voraussetzungen auf Ihrer lokalen Maschine installiert sind und ordnungsgemäß funktionieren, bevor Sie Cluster-Management-Tasks ausführen.

1. Installieren und konfigurieren Sie die folgenden Befehlszeilentools:

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0 oder höher, einschließlich der Befehlszeilenschnittstelle von IBM Cloud Private: [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 oder höher: [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 oder höher: [`helm`](https://helm.sh){: external}

1.  Starten Sie `helm`:
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  Führen Sie die folgenden Testbefehle aus, um zu überprüfen, ob die Tools ordnungsgemäß installiert sind. 

    - Testen Sie die Befehlszeilenschnittstelle von IBM Cloud Private (`cloudctl`):

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}
    
      Wenn Sie eine Lastausgleichsfunktion verwenden, geben Sie den Hostnamen der Lastausgleichsfunktion anstelle des Hostnamens des Masterknotens an.
      {: note}

    - Testen Sie Kubernetes (`kubectl`):

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      Wenn Sie den Befehl `kubectl` nicht ausführen können, lesen Sie den Abschnitt [Zugriff auf die Kubernetes-Befehlszeilenschnittstelle einrichten](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}.
      {: note}

    - Testen Sie Helm (`helm`):

      ```bash
      helm version --tls
      ```
      {: pre}

## Management-Tasks ausführen
{: perform-mgmt-tasks}

Die folgende Liste enthält einige der Tasks, die Sie zur Überwachung und Verwaltung Ihrer {{site.data.keyword.texttospeechshort}}-Instanz ausführen können.

  - Clusterknoten identifizieren, auf denen das Produkt bereitgestellt ist:
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - Die Anzahl der Replikate jedes Mikroservice in einem bestimmten Namensbereich (`{namespace}`) auflisten:
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    oder
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - Die Anzahl der Replikate erhöhen oder verringern:
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    oder
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - Protokolle anzeigen

    Standardmäßig protokolliert {{site.data.keyword.icp4dfull_notm}} Informationen aus jedem Service automatisch. Weitere Informationen finden Sie in [Protokolle anzeigen](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}.

## Benutzerzugriff verwalten
{: #manage-user-access}

Nach der Bereitstellung einer Instanz können Sie die URL für den Service mit anderen Benutzern gemeinsam nutzen. Diese Benutzer können sich jedoch nur dann bei dem Service anmelden, wenn Sie ihnen Zugriff gewähren. 

Wenn Sie SAML für Single Sign-on (SSO) verwenden wollen, führen Sie die in [Single Sign-on konfigurieren](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) beschriebenen Schritte aus, bevor Sie Benutzer hinzufügen. Wenn Sie Benutzer hinzufügen, bevor Sie SSO konfigurieren, müssen Sie die Benutzer mit ihren SAML-IDs erneut hinzufügen, damit sie SSO verwenden können.

1.  Klicken Sie im Web-Client-Menü auf **Verwalten > Benutzer verwalten**.

1.  Klicken Sie auf **Benutzer hinzufügen** und geben Sie dann den vollständigen Namen, den Benutzernamen und die E-Mail-Adresse des Benutzers an. Legen Sie die Berechtigungen des Benutzers fest und klicken Sie anschließend auf **Hinzufügen**.

1.  Wählen Sie im Web-Client-Menü **Eigene Instanzen**aus.

1.  Suchen Sie Ihre {{site.data.keyword.texttospeechshort}}-Instanz, klicken Sie auf **...** und wählen Sie anschließend **Zugriff verwalten** aus.

1.  Klicken Sie auf **Benutzer hinzufügen**.

1.  Klicken Sie auf das Benutzernamensfeld, um eine Liste der Benutzer anzuzeigen, die Sie hinzufügen können.

    Die im vorherigen Schritt hinzugefügten Benutzer werden aufgelistet. Wählen Sie einen Namen und dann **Benutzer** oder **Administrator** als Zugriffsrolle aus. Klicken Sie anschließend auf **Hinzufügen**. 

    Wenn Sie nicht mit einer vorhandenen Benutzerregistry verbunden sind und Single Sign-on nicht aktiviert haben, werden für die von Ihnen hinzugefügten Benutzer temporäre Kennwörter erstellt. Die temporären Kennwörter werden über die von Ihnen angegebenen E-Mail-Adressen an Benutzer gesendet.
