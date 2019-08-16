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

# 管理集群
{: #manage}

在 {{site.data.keyword.icp4dfull}} 上安装和配置 {{site.data.keyword.texttospeechdatafull}} 之后，即可管理实例和集群。

## 准备本地计算机
{: #manage-prep-local-machine}

确保已安装下列必备软件并且在本地计算机上正常运行，然后再执行集群管理任务。

1. 安装和配置以下命令行工具：

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0 或更高版本，包括 IBM Cloud Private CLI：[`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 或更高版本：[`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 或更高版本：[`helm`](https://helm.sh){: external}

1.  启动 `helm`：
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  通过运行以下测试命令来验证是否已正确安装工具。

    - 测试 IBM Cloud Private CLI (`cloudctl`)：

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}
    
      如果要使用负载均衡器，请指定负载均衡器的主机名，而不是主节点的主机名。
      {: note}

    - 测试 Kubernetes (`kubectl`)：

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      如果无法运行 `kubectl` 命令，请参阅[启用对 Kubernetes 命令行界面的访问](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}。
      {: note}

    - 测试 Helm (`helm`)：

      ```bash
      helm version --tls
      ```
      {: pre}

## 执行管理任务
{: perform-mgmt-tasks}

下面是您可以执行的一些任务，可用于监视和维护 {{site.data.keyword.texttospeechshort}} 实例。

  - 识别将产品部署到的集群节点：
```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - 列出给定 `{namespace}` 中每个微型服务的副本数：
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
或者
```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - 更改（增加或减少）副本数：
```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
或者
```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - 查看日志

    缺省情况下，{{site.data.keyword.icp4dfull_notm}} 会自动记录每个服务的信息。有关更多信息，请参阅[查看日志](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}。

## 管理用户访问权
{: #manage-user-access}

在供应实例之后，可以与其他用户共享服务的 URL。但那些用户只有在获得您的授权后才能登录服务。

如果您计划将 SAML 用于单点登录 (SSO)，请先完成[配置单点登录](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso)，然后再添加用户。如果您在配置 SSO 之前添加用户，那么需要使用用户 SAML 标识重新添加用户，才能支持用户使用 SSO。

1.  在 Web 客户机菜单中，单击**管理 > 管理用户**。

1.  单击**添加用户**，然后指定用户的全名、用户名和电子邮件地址。设置用户许可权，然后单击**添加**。

1.  在 Web 客户机菜单中，选择**我的实例**。

1.  找到 {{site.data.keyword.texttospeechshort}} 实例，单击更多 (**...**) 菜单，然后选择**管理访问权**。

1.  单击**添加用户**。

1.  单击用户名字段以查看您可以添加的人员列表。

    此时会列出您在先前步骤中添加的用户。选择一个名称，选择**用户**或**管理员**作为其访问角色，然后单击**添加**。 

    如果未连接到现有用户注册表，并且未启用单点登录，那么会为您添加的用户创建临时密码。临时密码会通过您指定的电子邮件地址发送给用户。
