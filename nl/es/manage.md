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

# Gestión del clúster
{: #manage}

Después de instalar y configurar {{site.data.keyword.texttospeechdatafull}} en {{site.data.keyword.icp4dfull}}, puede gestionar la instancia y el clúster.

## Preparación de la máquina local
{: #manage-prep-local-machine}

Asegúrese de que tiene los siguientes requisitos previos instalados y que funcionan correctamente en la máquina local antes de realizar las tareas de gestión de clúster.

1. Instale y configure las siguientes herramientas de línea de mandatos:

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0 o posterior, incluida la CLI de IBM Cloud Private: [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 o posterior: [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 o posterior: [`helm`](https://helm.sh){: external}

1.  Inicie `helm`:
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  Verifique que las herramientas se han instalado correctamente ejecutando los mandatos de prueba siguientes.

    - Pruebe la CLI IBM Cloud Private (`cloudctl`):

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}
    
      Si está utilizando un equilibrador de carga, especifique el nombre de host del equilibrador de carga en lugar del nombre de host del nodo maestro.
      {: note}

    - Probar Kubernetes (`kubectl`):

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      Si no puede ejecutar el mandato `kubectl`, consulte [Habilitación del acceso a la interfaz de línea de mandatos de Kubernetes](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}.
      {: note}

    - Probar Helm (`helm`):

      ```bash
      helm version --tls
      ```
      {: pre}

## Realización de tareas de gestión
{: perform-mgmt-tasks}

A continuación se indican algunas de las tareas que se pueden realizar para supervisar y mantener la instancia de {{site.data.keyword.texttospeechshort}}.

  - Identifique los nodos de clúster a los que se despliega el producto:
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - Listar el número de réplicas de cada microservicio en un `{namespace}` dado:
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    o bien
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - Cambiar (aumentar o disminuir) el número de réplicas:
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    o bien
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - Ver registros

    De forma predeterminada, {{site.data.keyword.icp4dfull_notm}} registra automáticamente información de cada servicio. Para obtener más información, consulte [Visualización de registros](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}.

## Gestión de acceso de usuario
{: #manage-user-access}

Después de suministrar una instancia, puede compartir el URL del servicio con otros usuarios. Sin embargo, estos usuarios pueden iniciar sesión en el servicio sólo si les da acceso.

Si tiene pensado utilizar SAML para inicio de sesión único (SSO), complete la [Configuración del inicio de sesión único](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) antes de añadir usuarios. Si añade usuarios antes de configurar SSO, tendrá que volver a añadirlos con sus ID de SAML para que puedan utilizar SSO.

1.  En el menú del cliente web, pulse **Administrar > Gestionar usuarios**.

1.  Pulse **Añadir usuario** y, a continuación, especifique el nombre completo, el nombre de usuario y la dirección de correo electrónico del usuario. Establezca los permisos del usuario y, a continuación, pulse **Añadir**.

1.  En el menú del cliente web, seleccione **Mis instancias**.

1.  Busque la instancia de {{site.data.keyword.texttospeechshort}}, pulse el menú de más opciones (**...**) y, a continuación, seleccione **Gestionar acceso**.

1.  Pulse **Añadir usuario**.

1.  Pulse en el campo de nombre de usuario para ver una lista de las personas que puede añadir.

    Se listan los usuarios que ha añadido en los pasos anteriores. Seleccione un nombre, elija **Usuario** o **Admin** como su rol de acceso y, a continuación, pulse **Añadir**. 

    Si no está conectado a un registro de usuarios existente y no ha habilitado el inicio de sesión único, se crean contraseñas temporales para los usuarios que añada. Las contraseñas temporales se envían a los usuarios a través de las direcciones de correo electrónico que ha especificado.
