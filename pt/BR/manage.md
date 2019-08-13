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

# Gerenciando o cluster
{: #manage}

Após você instalar e configurar o {{site.data.keyword.texttospeechdatafull}} no {{site.data.keyword.icp4dfull}}, será possível gerenciar a instância e o cluster.

## Preparando a sua máquina local
{: #manage-prep-local-machine}

Assegure-se de que você tenha os pré-requisitos a seguir instalados e funcionando corretamente em sua máquina local antes de executar qualquer tarefa de gerenciamento de cluster.

1. Instale e configure as ferramentas de linha de comandos a seguir:

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0 ou mais recente, incluindo a CLI do IBM Cloud Private: [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 ou mais recente: [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 ou mais recente: [`helm`](https://helm.sh){: external}

1.  Inicie o `helm`:
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  Verifique se as ferramentas estão instaladas corretamente, executando os comandos de teste a seguir.

    - Teste a CLI do IBM Cloud Private (`cloudctl`):

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}
    
      Se você estiver usando um balanceador de carga, especifique o nome do host do balanceador de carga em vez do nome do host do nó principal.
      {: note}

    - Testar o Kubernetes (`kubectl`):

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      Se não for possível executar o comando `kubectl`, consulte [Ativando o acesso à interface da linha de comandos do Kubernetes](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}.
      {: note}

    - Testar o Helm (`helm`):

      ```bash
      helm version --tls
      ```
      {: pre}

## Executando tarefas de gerenciamento
{: perform-mgmt-tasks}

A seguir estão algumas das tarefas que podem ser executadas para monitorar e manter a sua instância do {{site.data.keyword.texttospeechshort}}.

  - Identificar os nós do cluster para os quais o produto está implementado:
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - Listar o número de réplicas de cada microsserviço em um determinado `{namespace}`:
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    ou
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - Mudar (aumentar ou diminuir) o número de réplicas:
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    ou
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - Visualizar Logs

    Por padrão, o {{site.data.keyword.icp4dfull_notm}} registra automaticamente as informações de cada serviço. Para obter mais informações, consulte  [ Visualizando logs ](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}.

## Gerenciando o acesso de usuário
{: #manage-user-access}

Depois de fornecer uma instância, é possível compartilhar a URL para o serviço com outros usuários. No entanto, esses usuários poderão efetuar login no serviço somente se você lhes der acesso.

Se você planejar usar o SAML para conexão única (SSO), conclua [Configurando a conexão única](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) antes de incluir usuários. Se você incluir usuários antes de configurar a SSO, será necessário incluir novamente os usuários com seus IDs de SAML para permitir que eles usem a SSO.

1.  No menu do Web client, clique em **Administrar > Gerenciar usuário**.

1.  Clique em **Incluir usuário** e, em seguida, especifique o nome completo do usuário, o nome do usuário e o endereço de e-mail. Configure as permissões do usuário e, em seguida, clique em **Incluir**.

1.  No menu do Web client, selecione **Minhas instâncias**.

1.  Localize a sua instância do {{site.data.keyword.texttospeechshort}}, clique no menu mais (**...**) e, em seguida, escolha **Gerenciar acesso**.

1.  Clique em **Incluir usuário**.

1.  Clique no campo de nome do usuário para ver uma lista de pessoas que você pode incluir.

    Os usuários que você incluiu nas etapas anteriores são listados. Selecione um nome, escolha **Usuário** ou **Administrador** como sua função de acesso e, em seguida, clique em **Incluir**. 

    Se você não estiver conectado a um registro de usuário existente e não tiver ativado a conexão única, as senhas temporárias serão criadas para os usuários que você incluir. As senhas temporárias são enviadas para os usuários por meio dos endereços de e-mail que você especificou.
