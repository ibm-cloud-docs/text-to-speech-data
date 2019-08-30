---

copyright:
  years: 2019
lastupdated: "2019-08-28"

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

# Managing the cluster
{: #manage}

After you install and configure {{site.data.keyword.texttospeechdatafull}} on {{site.data.keyword.icp4dfull}}, you can manage the instance and the cluster.

## Preparing your local machine
{: #manage-prep-local-machine}

Ensure that you have the following prerequisites installed and working correctly on your local machine before performing any cluster-management tasks.

1. Install and configure the following command-line tools:

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0.1 or later, including the IBM Cloud Private CLI: [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 or later: [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 or later: [`helm`](https://helm.sh){: external}

1.  Start `helm`:

    ```bash
    helm init --client-only
    ```
    {: pre}

1.  Verify that the tools are installed correctly by running the following test commands.

    - Test the IBM Cloud Private CLI (`cloudctl`):

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}

      If you are using a load balancer, specify the hostname of the load balancer instead of the hostname of the master node.
      {: note}

    - Test Kubernetes (`kubectl`):

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      If you cannot run the `kubectl` command, see [Enabling access to the Kubernetes command-line interface](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}.
      {: note}

    - Test Helm (`helm`):

      ```bash
      helm version --tls
      ```
      {: pre}

## Performing management tasks
{: perform-mgmt-tasks}

The following are some of the tasks you can perform to monitor and maintain your {{site.data.keyword.texttospeechshort}} instance.

  - Identify the cluster nodes to which the product is deployed:
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - List the number of replicas of each microservice in a given `{namespace}`:
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    or
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - Change (increase or decrease) the number of replicas:
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    or
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - View logs

    By default, {{site.data.keyword.icp4dfull_notm}} automatically logs information from each service. For more information, see [Viewing logs](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}.

## Managing user access
{: #manage-user-access}

After you provision an instance, you can share the URL for the service with other users. However, those users can  log in to the service only if you give them access.

If you plan to use SAML for single sign-on (SSO), complete [Configuring single sign-on](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) before you add users. If you add users before you configure SSO, you need to re-add the users with their SAML IDs to enable them to use SSO.

1.  From the web client menu, click **Administer > Manage user**.

1.  Click **Add user**, then specify the user's full name, user name, and email address. Set the user's permissions, and then click **Add**.

1.  From the web client menu, select **My Instances**.

1.  Find your {{site.data.keyword.texttospeechshort}} instance, click the more (**...**) menu, and then choose **Manage Access**.

1.  Click **Add user**.

1.  Click the user name field to see a list of the people you can add.

    The users you added in the previous steps are listed. Select a name, choose **User** or **Admin** as their access role, and then click **Add**.

    If you are not connected to an existing user registry and have not enabled single sign-on, then temporary passwords are created for the users you add. The temporary passwords are sent to users by way of the email addresses you specified.

## Performing management tasks
{: perform-mgmt-tasks}

The following are some of the tasks you can perform to monitor and maintain your {{site.data.keyword.texttospeechshort}} instance.

  - Identify the cluster nodes to which the product is deployed:
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - List the number of replicas of each microservice in a given `{namespace}`:
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    or
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - Change (increase or decrease) the number of replicas:
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    or
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - View logs

    By default, {{site.data.keyword.icp4dfull_notm}} automatically logs information from each service. For more information, see [Viewing logs](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}.

## Managing user access
{: #manage-user-access}

After you provision an instance, you can share the URL for the service with other users. However, those users can  log in to the service only if you give them access.

If you plan to use SAML for single sign-on (SSO), complete [Configuring single sign-on](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) before you add users. If you add users before you configure SSO, you need to re-add the users with their SAML IDs to enable them to use SSO.

1.  From the web client menu, click **Administer > Manage user**.

1.  Click **Add user**, then specify the user's full name, user name, and email address. Set the user's permissions, and then click **Add**.

1.  From the web client menu, select **My Instances**.

1.  Find your {{site.data.keyword.texttospeechshort}} instance, click the more (**...**) menu, and then choose **Manage Access**.

1.  Click **Add user**.

1.  Click the user name field to see a list of the people you can add.

    The users you added in the previous steps are listed. Select a name, choose **User** or **Admin** as their access role, and then click **Add**. 

    If you are not connected to an existing user registry and have not enabled single sign-on, then temporary passwords are created for the users you add. The temporary passwords are sent to users by way of the email addresses you specified.

## Creating custom certificate secrets

For information about creating custom certificate secrets, see [Installing the Watson Text to Speech add-on](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/watson/text-to-speech-install.html){: external}.

## Scaling deployments and StatefulSets
{: #scaling}

For information about scaling deployments and StatefulSets, see [Installing the Watson Text to Speech add-on](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/watson/text-to-speech-install.html){: external}.

## Viewing logs from the {{site.data.keyword.icp4dfull_notm}} Logging dashboard
{: #viewing-logs}

1. Make sure an ELK stack is deployed to your cluster. For more information, see [IBM Cloud Private Logging](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/manage_metrics/logging_elk.html).

2. Log in to the console of your cluster by accessing `https://{cluster_CA_domain}:8443` in your Web browser.

    - `{cluster_CA_domain}`: your cluster CA domain name; for example, `mycluster.icp`.

3. Open Kibana by accessing *Side Menu -> Platform -> Logging*

4. To view and query logs, see [Viewing and querying logs](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/manage_metrics/logging_elk.html#viewing-and-querying-logs).

    - To view all of your installation logs, use the `kubernetes.pod:"{release_name}-*` command, where `{release name}` is the Helm release name of your installation. To identify the component output of a log, check the `kubernetes.pod` field of the log to see the pod name and look up the component with the pod name in the table in [Deployments](#deployments).

    - To view the logs of a specific deployment, use the `kubernetes.pod:"{deployment_name}-*"` command, where `{deployment_name}` is the Kubernetes deployment name of the component whose logs you want to view. See [Deployments](#deployments) for the deployment name of each component. 
