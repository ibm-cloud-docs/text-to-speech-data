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

# 管理叢集
{: #manage}

在 {{site.data.keyword.icp4dfull}} 上安裝和配置 {{site.data.keyword.texttospeechdatafull}} 之後，即可管理實例和叢集。

## 準備本端機器
{: #manage-prep-local-machine}

請確定已安裝下列必要條件並且在本端機器上正常運作，然後再執行任何叢集管理作業。

1. 安裝和配置下列指令行工具：

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0 或更高版本，包括 IBM Cloud Private CLI：[`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 或更高版本：[`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 或更高版本：[`helm`](https://helm.sh){: external}

1.  啟動 `helm`：
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  執行下列測試指令來驗證是否已正確安裝工具。

    - 測試 IBM Cloud Private CLI (`cloudctl`)：

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}
    
      如果使用負載平衡器，請指定負載平衡器的主機名稱，而不是主節點的主機名稱。
      {: note}

    - 測試 Kubernetes (`kubectl`)：

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      如果無法執行 `kubectl` 指令，請參閱[啟用對 Kubernetes 指令行介面的存取](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}。
      {: note}

    - 測試 Helm (`helm`)：

      ```bash
      helm version --tls
      ```
      {: pre}

## 執行管理作業
{: perform-mgmt-tasks}

以下是您可以執行的一些作業，可用於監視和維護 {{site.data.keyword.texttospeechshort}} 實例。

  - 識別將產品部署到的叢集節點：
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - 列出給定 `{namespace}` 中每個微服務的抄本數：
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    或
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - 變更（增加或減少）抄本數：
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    或
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - 檢視日誌

    依預設，{{site.data.keyword.icp4dfull_notm}} 會自動記載每個服務的資訊。如需相關資訊，請參閱[檢視日誌](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}。

## 管理使用者存取權
{: #manage-user-access}

在佈建實例之後，可以與其他使用者共用服務的 URL。但那些使用者只有在獲得您的授權後才能登入服務。

如果您計劃將 SAML 用於單一登入 (SSO)，請先完成[配置單一登入](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso)，然後再新增使用者。如果您在配置 SSO 之前新增使用者，您需要以使用者 SAML ID 重新新增使用者，他們才能使用 SSO。

1.  在 Web 用戶端功能表中，按一下**管理 > 管理使用者**。

1.  按一下**新增使用者**，然後指定使用者的完整名稱、使用者名稱和電子郵件位址。設定使用者許可權，然後按一下**新增**。

1.  在 Web 用戶端功能表中，選取**我的實例**。

1.  找到 {{site.data.keyword.texttospeechshort}} 實例，按一下更多 (**...**) 功能表，然後選擇**管理存取權**。

1.  按一下**新增使用者**。

1.  按一下使用者名稱欄位以查看您可以新增的人員清單。

    此時會列出您在先前步驟中新增的使用者。選取一個名稱，選取**使用者**或**管理**作為其存取角色，然後按一下**新增**。 

    如果未連接至現有使用者登錄，並且未啟用單一登入，則會為您新增的使用者建立臨時密碼。臨時密碼會藉由您指定的電子郵件位址傳送給使用者。
