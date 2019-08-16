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

# 클러스터 관리
{: #manage}

{{site.data.keyword.icp4dfull}}에 {{site.data.keyword.texttospeechdatafull}}를 설치한 후에 인스턴스 및 클러스터를 관리할 수 있습니다.

## 로컬 머신 준비
{: #manage-prep-local-machine}

클러스터 관리 태스크를 수행하기 전에 다음 필수 소프트웨어가 설치되어 있으며 로컬 시스템에서 제대로 작동하고 있는지 확인하십시오.

1. 다음 명령행 도구 설치를 및 구성하십시오.

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0 이상(IBM Cloud Private CLI 포함): [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 이상: [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 이상: [`helm`](https://helm.sh){: external}

1.  `helm`을 시작하십시오.
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  다음 테스트 명령을 실행하여 도구가 올바르게 설치되었는지 확인하십시오.

    - IBM Cloud Private CLI 테스트(`cloudctl`):

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}
    
      로드 밸런서를 사용하는 경우, 마스터 노드의 호스트 이름 대신 로드 밸런서의 호스트 이름을 지정하십시오.
      {: note}

    - Kubernetes 테스트(`kubectl`):

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      `kubectl` 명령을 실행할 수 없으면 [Kubernetes 명령행 인터페이스에 대한 액세스 사용](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}을 참조하십시오.
      {: note}

    - Helm 테스트(`helm`):

      ```bash
      helm version --tls
      ```
      {: pre}

## 관리 태스크 수행
{: perform-mgmt-tasks}

다음은 {{site.data.keyword.texttospeechshort}} 인스턴스를 모니터하고 유지보수하기 위해 수행할 수 있는 몇 가지 태스크입니다.

  - 제품이 배치되는 클러스터 노드 식별:
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - 지정된 `{namespace}`에 각 마이크로서비스의 복제본 수 나열:
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    또는
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - 복제본의 수 변경(늘리기 또는 줄이기):
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    또는
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - 로그 보기

    기본적으로 {{site.data.keyword.icp4dfull_notm}}는 자동으로 각 서비스에서 정보를 로깅합니다. 자세한 정보는 [로그 보기](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}를 참조하십시오.

## 사용자 액세스 관리
{: #manage-user-access}

인스턴스를 프로비저닝한 다음 다른 사용자와 서비스에 대한 URL을 공유할 수 있습니다. 단, 사용자가 액세스 권한을 부여한 경우에만 해당 사용자가 서비스에 로그인할 수 있습니다.

싱글 사인온(SSO)을 위해 SAML을 사용할 계획이라면 사용자를 추가하기 전에 [싱글 사인온 구성](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso)을 완료하십시오. SSO를 구성하기 전에 사용자를 추가한 경우, 해당 사용자가 SSO를 사용하도록 설정하려면 SAML ID를 사용하여 사용자를 다시 추가해야 합니다.

1.  웹 클라이언트 메뉴에서 **관리자 > 사용자 관리**를 클릭하십시오.

1.  **사용자 추가**를 클릭한 다음 사용자의 전체 이름, 사용자 이름 및 이메일 주소를 지정하십시오. 사용자의 권한을 설정하고 **추가**를 클릭하십시오.

1.  웹 클라이언트 메뉴에서 **내 인스턴스**를 선택하십시오.

1.  {{site.data.keyword.texttospeechshort}} 인스턴스를 찾고 자세히 보기(**...**) 메뉴를 클릭한 다음 **액세스 관리**를 선택하십시오.

1.  **사용자 추가**를 클릭하십시오.

1.  사용자 이름 필드를 클릭하여 추가할 수 있는 사람 목록을 보십시오.

    이전 단계에서 추가한 사용자가 나열됩니다. 이름을 선택하고 액세스 역할로 **사용자** 또는 **관리자**를 선택한 다음 **추가**를 클릭하십시오. 

    기존 사용자 레지스트리에 연결되어 있지 않으며 싱글 사인온을 사용할 수 없는 경우에는 추가한 사용자를 위해 임시 비밀번호가 작성됩니다. 임시 비밀번호는 사용자가 지정한 이메일 주소를 사용하여 사용자에게 전송됩니다.
