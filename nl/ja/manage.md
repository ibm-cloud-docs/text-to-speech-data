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

# クラスターの管理
{: #manage}

{{site.data.keyword.texttospeechdatafull}} を {{site.data.keyword.icp4dfull}} にインストールして構成した後に、インスタンスとクラスターの管理を行うことができます。

## ローカル・マシンの準備
{: #manage-prep-local-machine}

クラスター管理の作業を実行する前に、以下の前提条件がローカル・マシンにインストールされていて、正常に機能していることを確認してください。

1. 以下のコマンド・ライン・ツール製品をインストールして構成します。

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0 以降 (IBM Cloud Private CLI を含む): [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 以降: [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 以降: [`helm`](https://helm.sh){: external}

1.  以下のようにして、`helm` を開始します。
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  以下のテスト・コマンドを実行して、ツールが正常にインストールされたことを確認します。

    - IBM Cloud Private CLI (`cloudctl`) をテストします。

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}
    
      ロード・バランサーを使用している場合、マスター・ノードのホスト名ではなくロード・バランサーのホスト名を指定します。
      {: note}

    - Kubernetes (`kubectl`) をテストします。

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      `kubectl` コマンドを実行できない場合は、[Enabling access to the Kubernetes command-line interface](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external} を参照してください。
      {: note}

    - Helm (`helm`) をテストします。

      ```bash
      helm version --tls
      ```
      {: pre}

## 管理タスクの実行
{: perform-mgmt-tasks}

以下は、{{site.data.keyword.texttospeechshort}} インスタンスをモニターして保守するために実行できるいくつかの作業です。

  - 製品のデプロイ先のクラスター・ノードを識別します。
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - 指定の `{namespace}` にある各マイクロサービスのレプリカ数をリストします。
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    または
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - レプリカの数を変更 (増加または減少) します。
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    または
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - ログを表示します

    デフォルトで、{{site.data.keyword.icp4dfull_notm}} は各サービスからの情報を自動的にログに記録します。詳しくは、[Viewing logs](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external} を参照してください。

## ユーザーのアクセス権限の管理
{: #manage-user-access}

インスタンスをプロビジョンした後に、サービスの URL を他のユーザーと共有できます。ただし、それらのユーザーはアクセス権限を付与された場合にのみサービスにログインできます。

シングル・サインオン (SSO) 用に SAML を使用する予定の場合、ユーザーを追加する前に[シングル・サインオンの構成](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso)を行ってください。SSO を構成する前にユーザーを追加する場合は、それらのユーザーが SSO を使用できるようにするために、SAML ID を指定してユーザーを再度追加することが必要になります。

1.  Web クライアントのメニューから、**「管理 (Administer)」>「ユーザーの管理」**をクリックします。

1.  **「ユーザーの追加」**をクリックしてから、ユーザーのフルネーム、ユーザー名、および E メール・アドレスを指定します。ユーザーの許可を設定して、**「追加 (Add)」**をクリックします。

1.  Web クライアントのメニューから、**「マイ・インスタンス (My Instances)」**を選択します。

1.  ユーザーの {{site.data.keyword.texttospeechshort}} インスタンスを見つけて、その他 (**...**) メニューをクリックし、**「アクセス管理」**を選択します。

1.  **「ユーザーの追加」**をクリックします。

1.  ユーザー名フィールドをクリックして、追加可能な個人のリストを表示します。

    以前のステップで追加したユーザーがリストされています。名前を選択して、そのアクセス役割として**「ユーザー」**または**「管理」**を選択し、**「追加 (Add)」**をクリックします。 

    既存のユーザー・レジストリーに接続していない場合で、シングル・サインオンを有効にしていなければ、追加したユーザー用に一時パスワードが作成されます。一時パスワードは、指定した E メール・アドレスを使用してユーザーに送信されます。
