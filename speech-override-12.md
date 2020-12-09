---

copyright:
  years: 2020
lastupdated: "2020-12-07"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:pre: .pre}
{:note: .note}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:gif: data-image-type='gif'}

# Using the override file
{: #speech-override-12}

You can use the `speech-override.yaml` file to customize many aspects of your {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} installation. The installation procedure in the IBM Knowledge Center shows an abbreviated example of the `speech-override.yaml` file. But an override file can include many more installation and configuration values.

## The speech-override.yaml file
{: #speech-override-file-12}

The following example duplicates the `speech-override.yaml` example from [Creating an override file for {{site.data.keyword.watson}} {{site.data.keyword.speechtotextshort}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-speech/stt-svc-override.html){: external} and [Creating an override file for {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-text/tts-svc-override.html){: external}. The sections that follow describe the values that you can use to modify and augment the file. You can download a complete copy of the [speech-override.yaml](https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/cpd-version-12/speech-override.yaml){: external} file.

```yaml
tags:
  sttAsync: true
  sttCustomization: true
  ttsCustomization: true
  sttRuntime: true
  ttsRuntime: true

affinity: {}

global:
  dockerRegistryPrefix: "{Registry}"
  image:
    pullSecret: "{Registry_pull_secret}"
    pullPolicy: "IfNotPresent"

  datastores:

    minio:
      tlsEnabled: true
      serviceAccountName: "ibm-minio-operator"

      #Images
      images:
        certgen:
          name: opencontent-icp-cert-gen-1
          tag: 1.1.9
        minio:
          name: "opencontent-minio"
          tag: 1.1.5
        minioClient:
          name: "opencontent-minio-client"
          tag: 1.0.5

      #Sizing
      deploymentType: Development #Development or Production

      # 4 <= Replicas <= 32
      replicasForDev: 4
      replicasForProd: 4

      memoryLimit: 2048Mi
      cpuRequest: 250m
      cpuLimit: 500m
      memoryRequest: 256Mi

      #Storage
      storageClassName: "portworx-sc"

      #Secrets
      authSecretName: minio
      tlsSecretName: "{{ .Release.Name }}-ibm-datastore-tls"

    rabbitMQ:
      tlsEnabled: true
      replicas: 3

      #Images
      images:
        config:
          name: opencontent-rabbitmq-config-copy
          tag: 1.1.5
        rabbitmq:
          name: opencontent-rabbitmq-3
          tag: 1.1.8

      #Sizing
      cpuRequest: 200m
      cpuLimit: 200m
      memoryRequest: 256Mi
      memoryLimit: 256Mi

      #Storage
      storageClassName: "portworx-sc"
      pvEnabled: true
      pvSize: 5Gi
      useDynamicProvisioning: true

      #Secrets
      tlsSecretName: "{{ .Release.Name }}-ibm-datastore-tls"
      authSecretName: "{{ .Release.Name }}-ibm-rabbitmq-auth-secret"

    postgressql:
      tlsEnabled: true
      serviceAccount: "edb-operator"

      #Images
      images:
        stolon:
          name: "edb-stolon"
          tag: "v1-ubi8-amd64"
        postgres:
          name: "edb-postgresql-12"
          tag: "ubi8-amd64"

      #Sizing configuration
      replicas: 3
      databaseMemoryLimit: "5Gi"
      databaseMemoryRequest: "1Gi"
      databaseCPULimit: "1000m"
      databaseCPU: "50m"
      databaseStorageRequest: "5Gi"

      #Storage configuration
      databaseStorageClass: "portworx-sc"
      databaseArchiveStorageClass: "portworx-sc"
      databaseWalStorageClass: "portworx-sc"
      databasePort: 5432

      #Secrets
      authSecretName: "user-provided-postgressql"
      tlsSecretName: "{{ .Release.Name }}-ibm-datastore-tls"

  sttModels:
    enUsBroadbandModel:
      enabled: true
      catalogName: en-US_BroadbandModel
    enUsNarrowbandModel:
      enabled: true
      catalogName: en-US_NarrowbandModel
    enUsShortFormNarrowbandModel:
      enabled: true
      catalogName: en-US_ShortForm_NarrowbandModel

  ttsVoices:
    enUSMichaelV3Voice:
      enabled: true
      catalogName: en-US_MichaelV3Voice
    enUSLisaV3Voice:
      enabled: true
      catalogName: en-US_LisaV3Voice
    enUSAllisonV3Voice:
      enabled: true
      catalogName: en-US_AllisonV3Voice
```
{: codeblock}

You replace the following variable values in the file:

-   `{Registry}` is the address of the internal Red Hat&reg; OpenShift&reg; Docker registry. The value is one of the following:
    -   `image-registry.openshift-image-registry.svc:5000` for OpenShift 4.x.
    -   `docker-registry.default.svc:5000` for OpenShift 3.x.
-   `{Registry_pull_secret}` is the pull secret for the internal Docker registry, which you can learn by running the following command:

    ```bash
    oc get secrets | grep default-dockercfg
    ```
    {: pre}

## Override values for both Speech services
{: #speech-override-both-12}

The following sections describe override values that apply to both Speech services.

### Installing Speech services components
{: #speech-override-components-12}

The following five main components provide the base {{site.data.keyword.speechtotextshort}} and  {{site.data.keyword.texttospeechshort}} functionality. You can set these tags in the `speech-override.yaml` file to enable or disable the installation of each of the components.

By default, all of the components are enabled, but you can enable or disable them separately.

-   To install {{site.data.keyword.speechtotextshort}} only, set `ttsRuntime` and `ttsCustomization` to `false`.
-   To install  {{site.data.keyword.texttospeechshort}} only, set `sttRuntime`, `sttCustomization`, and `sttAsync` to `false`.
-   To install both {{site.data.keyword.speechtotextshort}} and  {{site.data.keyword.texttospeechshort}} without enabling customization, set `sttCustomization` and `ttsCustomization` to `false`.

Table 1 describes the top-level Speech components that you can install.

| Value | Installs ... | Default |
|-------|--------------|:-------:|
| `tags.sttRuntime` | {{site.data.keyword.speechtotextshort}} runtime component, the base component for speech recognition. This value enables the `/v1/recognize` interfaces (synchronous HTTP and WebSocket). Enabling any other {{site.data.keyword.speechtotextshort}} component automatically enables the {{site.data.keyword.speechtotextshort}} runtime component. For more information, see [The synchronous HTTP interface](/docs/speech-to-text-data?topic=speech-to-text-data-http) and [The WebSocket interface](/docs/speech-to-text-data?topic=speech-to-text-data-websockets). | `true` |
| `tags.sttAsync` | {{site.data.keyword.speechtotextshort}} asynchronous HTTP component. This value enables the `/v1/recognitions` interface. For more information, see [The asynchronous HTTP interface](/docs/speech-to-text-data?topic=speech-to-text-data-async). | `true` |
| `tags.sttCustomization` | {{site.data.keyword.speechtotextshort}} customization component. This value enables the `/v1/customizations` and `/v1/acoustic_customizations` interfaces for language model and acoustic model customization. Enabling it also enables the {{site.data.keyword.speechtotextshort}} runtime component if `tags.sttRuntime=false`. For more information, see [The customization interface](/docs/speech-to-text-data?topic=speech-to-text-data-customization). | `true` |
| `tags.ttsRuntime` | {{site.data.keyword.texttospeechshort}} runtime component, the base component for speech synthesis. This value enables the `/v1/synthesize` interfaces (HTTP and WebSocket). Enabling any other {{site.data.keyword.texttospeechshort}} component automatically enables the {{site.data.keyword.texttospeechshort}} runtime component. For more information, see [The HTTP interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingHTTP) and [The WebSocket interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingWebSocket). | `true` |
| `tags.ttsCustomization` | {{site.data.keyword.texttospeechshort}} customization component. This value enables the `/v1/customizations` interface for customization. Enabling it also enables the {{site.data.keyword.texttospeechshort}} runtime component if `tags.sttRuntime=false`. For more information, see [Understanding customization](/docs/text-to-speech-data?topic=text-to-speech-data-customIntro). | `true` |
{: caption="Table 1. Installation of Speech services components"}

### Specifying dynamic resource calculation
{: #speech-override-dynamic-12}

The {{site.data.keyword.speechtotextshort}} runtime, {{site.data.keyword.texttospeechshort}} runtime, and {{site.data.keyword.speechtotextshort}} customization AM patcher support dynamic memory resource calculation. The calculation is performed automatically based on the selected number of CPUs and the selected models and voices.

Dynamic resource calculation is enabled by default. You can modify this behavior by setting the values in Table 2 to `true` or `false` in the root of the override file. If you set any of these values to `false`, you must specify the required memory yourself.

Disabling dynamic resource allocation is not recommended and can cause undesired service behavior.
{: important}

| Value | Enables ... | Default |
|-------|-------------|:-------:|
| `sttRuntime.groups.sttRuntimeDefault.resources.dynamicMemory` | Dynamic resource calculation for the {{site.data.keyword.speechtotextshort}} runtime component. | `true` |
| `ttsRuntime.groups.ttsRuntimeDefault.resources.dynamicMemory` | Dynamic resource calculation for the {{site.data.keyword.texttospeechshort}} runtime component. | `true` |
| `sttAMPatcher.groups.sttAMPatcher.resources.dynamicMemory` | Dynamic resource calculation for the {{site.data.keyword.speechtotextshort}} customization AM patcher component. | `true` |
{: caption="Table 2. Configuration of dynamic resource calculation"}

### Specifying node affinity
{: #speech-override-affinity-12}

Node affinity for the Speech services pods enables you to constrain the nodes on which a pod can run based on the nodes' labels. The default affinity allows any pod to run on any amd64 node.

You can override the default specification by defining the `affinity` value in the `speech-override.yaml` file. For example, the following specification replaces the `affinity: {}` definition to enable affinity for the designated nodes.

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/e2e-az-name
          operator: In
          values:
          - e2e-az1
          - e2e-az2
```
{: codeblock}

### Anonymizing logs and audio data
{: #speech-override-anonymize-12}

You can anonymize your log and audio data for increased user privacy. Use the values in Table 3 to anonymize data that is stored by the different components. You can also disable the temporary storing of payload data in the running container. For more information, see [Disabling storage of user data](/docs/text-to-speech-data?topic=text-to-speech-data-speech-cluster-12#speech-cluster-customer-data-12).

| Value | Anonymizes ... | Default |
|-------|----------------|:-------:|
| `sttRuntime.anonymizeLogs` | {{site.data.keyword.speechtotextshort}} runtime logs and audio data. | `false` |
| `ttsRuntime.anonymizeLogs` | {{site.data.keyword.texttospeechshort}} runtime logs and audio data. | `false` |
| `sttAMPatcher.anonymizeLogs` | {{site.data.keyword.speechtotextshort}} customization acoustic model (AM) patcher runtime logs and audio data. | `false` |
{: caption="Table 3. Anonymization of logs and audio data"}

## Override values for datastores
{: #speech-override-datastores-12}

The following sections describe override values for the MinIO, RabbitMQ, and PostgreSQL datastores that apply to both Speech services. For more information about the datastores, see [Managing datastores](/docs/text-to-speech-data?topic=text-to-speech-data-speech-datastores-12) and [Scaling up your installation](/docs/text-to-speech-data?topic=text-to-speech-data-speech-scaling-12).

### Configuring the MinIO datastore
{: #speech-override-datastores-minio-12}

Table 4 describes the values that you can use to configure the MinIO datastore for your installation.

| Value | Specifies ... | Default |
|-------|---------------|:-------:|
| `global.datastores.minio.tlsEnabled` | Whether Transport Layer Security (TLS) is enabled for MinIO communications. | `true` |
| `global.datastores.minio.serviceAccountName` | MinIO service account name. | `"ibm-minio-operator"` |
| `global.datastores.minio.images.certgen.name` | Image name of MinIO certificate generation component. | `opencontent-icp-cert-gen-1` |
| `global.datastores.minio.images.certgen.tag` | Image tag of MinIO certificate generation component. | `1.1.9`
| `global.datastores.minio.images.minio.name` | Image name of Minio server component. | `"opencontent-minio"` |
| `global.datastores.minio.images.minio.tag` | Image tag of MinIO server component. | `1.1.5` |
| `global.datastores.minio.images.minioClient.name` | Image name of MinIO client component. | `"opencontent-minio-client"` |
| `global.datastores.minio.images.minioClient.tag` | Image tag of MinIO client component. | `1.0.5` |
| `global.datastores.minio.deploymentType` | Type of deployment configuration, `Development` or `Production`. | `Development` |
| `global.datastores.minio.replicasForDev` | Number of replica nodes for a Development configuration. Must be `4 <= x <= 32`. | `4` |
| `global.datastores.minio.replicasForProd` | Number of replica nodes for a Production configuration. Must be `4 <= x <= 32`. | `4` |
| `global.datastores.minio.memoryLimit` | Maximum memory that MinIO can use. | `2048Mi` |
| `global.datastores.minio.cpuRequest` | Minimum CPU requested by MinIO. | `250m` |
| `global.datastores.minio.cpuLimit` | Maximum CPU that MinIO can use. | `500m` |
| `global.datastores.minio.memoryRequest` | Minimum memory requested by MinIO. | `256Mi` |
| `global.datastores.minio.storageClassName` | Storage class that is used by MinIO. | `"portworx-sc"` |
| `global.datastores.minio.authSecretName` | Name of MinIO secrets object. | `minio` |
| `global.datastores.minio.tlsSecretName` | Name of TLS secrets object that MinIO uses. | `"{{ .Release.Name }}-ibm-datastore-tls"` |
{: caption="Table 4. Configuration of MinIO datastore"}

### Configuring the RabbitMQ datastore
{: #speech-override-datastores-rabbitmq-12}

Table 5 describes the values that you can use to configure the RabbitMQ datastore for your installation.

| Value | Specifies ... | Default |
|-------|---------------|:-------:|
| `global.datastores.rabbitMQ.tlsEnabled` | Whether TLS is enabled for RabbitMQ communications. | `true` |
| `global.datastores.rabbitMQ.replicas` | Number of replica nodes for RabbitMQ. | `3` |
| `global.datastores.rabbitMQ.images.config.name` | Image name of RabbitMQ configuration component. | `opencontent-rabbitmq-config-copy` |
| `global.datastores.rabbitMQ.images.config.tag` | Image tag of RabbitMQ configuration component. | `1.1.5`
| `global.datastores.rabbitMQ.images.rabbitmq.name` | Image name of RabbitMQ server component. | `opencontent-rabbitmq-3` |
| `global.datastores.rabbitMQ.images.rabbitmq.tag` | Image tag of RabbitMQ server component. | `1.1.8` |
| `global.datastores.rabbitMQ.cpuRequest` | Minimum CPU requested by RabbitMQ. | `200m` |
| `global.datastores.rabbitMQ.cpuLimit` | Maximum CPU that RabbitMQ can use. | `200m` |
| `global.datastores.rabbitMQ.memoryRequest` | Minimum memory requested by RabbitMQ. | `256Mi` |
| `global.datastores.rabbitMQ.memoryLimit` | Maximum memory that RabbitMQ can use. | `256Mi` |
| `global.datastores.rabbitMQ.storageClassName` | Storage class that is used by RabbitMQ. | `"portworx-sc"` |
| `global.datastores.rabbitMQ.pvEnabled` | Whether to store RabbitMQ on persistent volumes, which are preserved on pod restart. | `true` |
| `global.datastores.rabbitMQ.pvSize` | Size of the persistent volume for RabbitMQ. | `5Gi` |
| `global.datastores.rabbitMQ.useDynamicProvisioning` | Whether RabbitMQ uses dynamic provisioning. | `true` |
| `global.datastores.rabbitMQ.tlsSecretName` | Name of TLS secrets object that RabbitMQ uses. | `"{{ .Release.Name }}-ibm-datastore-tls"` |
| `global.datastores.rabbitMQ.authSecretName` | Name of RabbitMQ secrets object. | `"{{ .Release.Name }}-ibm-rabbitmq-auth-secret"` |
{: caption="Table 5. Configuration of RabbitMQ datastore"}

### Configuring the PostgreSQL datastore
{: #speech-override-datastores-postgresql-12}

Table 5 describes the values that you can use to configure the PostgreSQL datastore for your installation.

| Value | Specifies ... | Default |
|-------|---------------|:-------:|
| `global.datastores.postgressql.tlsEnabled` | Whether Transport Layer Security (TLS) is enabled for PostgresSQL communications. | `true` |
| `global.datastores.postgressql.serviceAccount` | PostgresSQL service account name. | `"edb-operator"` |
| `global.datastores.postgressql.images.stolon.name` | Image name of PostgreSQL Stolon architecture. | `"edb-stolon"` |
| `global.datastores.postgressql.images.stolon.tag` | Image tag of PostgreSQL Stolon architecture. | `"v1-ubi8-amd64"`
| `global.datastores.postgressql.images.postgressql.name` | Image name of PostgreSQL server component. | `"edb-postgresql-12"` |
| `global.datastores.postgressql.images.postgressql.tag` | Image tag of PostgreSQL server component. | `"ubi8-amd64"` |
| `global.datastores.postgressql.replicas` | Number of replica nodes for PostgreSQL. | `3` |
| `global.datastores.postgressql.databaseMemoryLimit` | Maximum memory that PostgreSQL can use. | `"5Gi"` |
| `global.datastores.postgressql.databaseMemoryRequest` | Minimum memory requested by PostgreSQL. | `"1Gi"` |
| `global.datastores.postgressql.databaseCPULimit` | Maximum CPU that PostgreSQL can use. | `"1000m"` |
| `global.datastores.postgressql.databaseCPU` | Minimum CPU requested by PostgreSQL. | `"50m"` |
| `global.datastores.postgressql.databaseStorageRequest` | Maximum size of a PostgreSQL database storage request. | `"5Gi"` |
| `global.datastores.postgressql.databaseStorageClass` | Storage class that is used by PostgreSQL for the database. | `"portworx-sc"` |
| `global.datastores.postgressql.databaseArchiveStorageClass` | Storage class for the Write-Ahead Log (WAL) archive directory to use. | `"portworx-sc"` |
| `global.datastores.postgressql.databaseWalStorageClass` | Storage class for the WAL directory to use. | `"portworx-sc"` |
| `global.datastores.postgressql.databasePort` | The port at which PostgreSQL listens for requests. | `5432` |
| `global.datastores.postgressql.authSecretName` | Name of PostgreSQL secrets object. | `"user-provided-postgressql"` |
| `global.datastores.postgressql.tlsSecretName` | Name of TLS secrets object that PostgreSQL uses. | `"{{ .Release.Name }}-ibm-datastore-tls"` |
{: caption="Table 6. Configuration of PostgreSQL datastore"}

## Override values for the {{site.data.keyword.speechtotextshort}} service
{: #speech-override-stt-12}

The following sections describe override values that are specific to the {{site.data.keyword.speechtotextshort}} service.

### Configuring the {{site.data.keyword.speechtotextshort}} runtime
{: #speech-override-stt-runtime-12}

Table 7 describes the configuration values for the {{site.data.keyword.speechtotextshort}} runtime.

| Value | Specifies ... | Default |
|-------|---------------|:-------:|
| `sttRuntime.groups.sttRuntimeDefault.resources.dynamicMemory` | Automatic calculation of the memory requirements for the {{site.data.keyword.speechtotextshort}} runtime according to the selected models. | `true` |
| `sttRuntime.groups.sttRuntimeDefault.resources.requestsCpu` | Requested CPUs for the {{site.data.keyword.speechtotextshort}} runtime. The minimum value is 4. Each runtime session needs at least 4 CPUs. | `8` |
| `sttRuntime.groups.sttRuntimeDefault.resources.requestsMemory` | Memory requirements for the {{site.data.keyword.speechtotextshort}} runtime. When dynamic memory is enabled, this value has no effect. | `22Gi` |
{: caption="Table 7. Configuration of {{site.data.keyword.speechtotextshort}} runtime"}

### Configuring the {{site.data.keyword.speechtotextshort}} customization AM patcher
{: #speech-override-stt-AMpatcher-12}

Table 8 describes the configuration values for the {{site.data.keyword.speechtotextshort}} customization AM patcher.

| Value | Specifies ... | Default |
|-------|---------------|:-------:|
| `sttAMPatcher.groups.sttAMPatcher.resources.dynamicMemory` | Automatic calculation of the memory requirements for the {{site.data.keyword.speechtotextshort}} customization AM patcher according to the selected models. | `true` |
| `sttAMPatcher.groups.sttAMPatcher.resources.requestsCpu` | Requested CPUs for the {{site.data.keyword.speechtotextshort}} customization AM patcher. The minimum value is 4. Each customization session needs at least 4 CPUs. | `8` |
| `sttAMPatcher.groups.sttAMPatcher.resources.requestsMemory` | Memory requirements for the {{site.data.keyword.speechtotextshort}} customization AM patcher. The amount of memory depends on the number of CPUs. The size can be calculated as the number of CPUs * 3 GB. | `22Gi` |
| `sttAMPatcher.groups.sttAMPatcher.resources.threads` | Number of parallel-processing threads for the {{site.data.keyword.speechtotextshort}} customization AM patcher. Note that fewer threads means longer training time. | `4` |
{: caption="Table 8. Configuration of {{site.data.keyword.speechtotextshort}} customization AM patcher"}

### Installing {{site.data.keyword.speechtotextshort}} models
{: #speech-override-stt-models-12}

You can use the values in Table 9 to specify the language models to install. Installing all models substantially increases the memory requirements. You are therefore strongly encouraged to install only those models and voices that you intend to use. By default, the dynamic resource calculation feature automatically computes the exact amount of memory that is required for the selected models.

You specify the models to be installed by setting the values in the `speech-override.yaml` file to `true` or `false`. For example, to install the Japanese, Korean, and Chinese language models (both broadband and narrowband) instead of the US English models, modify the `global.sttModels` values as follows:

```yaml
global:
  sttModels:
    enUsBroadbandModel:
      enabled: false
    enUsNarrowbandModel:
      enabled: false
    enUsShortFormNarrowbandModel:
      enabled: false
    jaJPBroadbandModel:
      enabled: true
    jaJPNarrowbandModel:
      enabled: true
    koKRBroadbandModel:
      enabled: true
    koKRNarrowbandModel:
      enabled: true
    zhCNBroadbandModel:
      enabled: true
    zhCNNarrowbandModel:
      enabled: true
```
{: codeblock}

For more information about all available models, see [Languages and models](/docs/speech-to-text-data?topic=speech-to-text-data-models). For information about updating the override file to install ad hoc models, see [Installing ad hoc models and voices](/docs/text-to-speech-data?topic=text-to-speech-data-speech-cluster-12#speech-cluster-model-install-adhoc-12).

| Value | Installs ... | Default |
|-------|--------------|:-------:|
| `global.sttModels.enUsBroadbandModel.enabled` | US English (`en-US`) Broadband model | `true` |
| `global.sttModels.enUsNarrowbandModel.enabled` | US English (`en-US`) Narrowband model | `true` |
| `global.sttModels.enUsShortFormNarrowbandModel.enabled` | US English (`en-US`) Short-Form Narrowband model | `true` |
| `global.sttModels.arArBroadbandModel.enabled` | Modern Standard Arabic (`ar-AR`) Broadband model | `false` |
| `global.sttModels.enAuBroadbandModel.enabled` | Australian English (`en-AU`) Broadband model | `false` |
| `global.sttModels.enAuNarrowbandModel.enabled` | Australian English (`en-AU`) Narrowband model | `false` |
| `global.sttModels.enGbBroadbandModel.enabled` | UK English (`en-GB`) Broadband model | `false` |
| `global.sttModels.enGbNarrowbandModel.enabled` | UK English (`en-GB`) Narrowband model | `false` |
| `global.sttModels.esEsBroadbandModel.enabled` | Spanish (`es-ES`, `es-AR`, `es-CL`, `es-CO`, `es-MX`, and `es-PE`) Broadband models | `false` |
| `global.sttModels.esEsNarrowbandModel.enabled` | Spanish (`es-ES`, `es-AR`, `es-CL`, `es-CO`, `es-MX`, and `es-PE`) Narrowband models | `false` |
| `global.sttModels.frFrBroadbandModel.enabled` | French (`fr-FR`) Broadband model | `false` |
| `global.sttModels.frFrNarrowbandModel.enabled` | French (`fr-FR`) Narrowband model | `false` |
| `global.sttModels.frCaBroadbandModel.enabled` | Canadian French (`fr-CA`) Broadband model | `false` |
| `global.sttModels.frCaNarrowbandModel.enabled` | Canadian French (`fr-CA`) Narrowband model | `false` |
| `global.sttModels.deDeBroadbandModel.enabled` | German (`de-DE`) Broadband model | `false` |
| `global.sttModels.deDeNarrowbandModel.enabled` | German (`de-DE`) Narrowband model | `false` |
| `global.sttModels.itItBroadbandModel.enabled` | Italian (`it-IT`) Broadband model | `false` |
| `global.sttModels.itItNarrowbandModel.enabled` | Italian (`it-IT`) Narrowband model | `false` |
| `global.sttModels.jaJpBroadbandModel.enabled` | Japanese (`ja-JP`) Broadband model | `false` |
| `global.sttModels.jaJpNarrowbandModel.enabled` | Japanese (`ja-JP`) Narrowband model | `false` |
| `global.sttModels.koKrBroadbandModel.enabled` | Korean (`ko-KR`) Broadband model | `false` |
| `global.sttModels.koKrNarrowbandModel.enabled` | Korean (`ko-KR`) Narrowband model | `false` |
| `global.sttModels.nlNlBroadbandModel.enabled` | Dutch (`nl-NL`) Broadband model | `false` |
| `global.sttModels.nlNlNarrowbandModel.enabled` | Dutch (`nl-NL`) Narrowband model | `false` |
| `global.sttModels.ptBrBroadbandModel.enabled` | Brazilian Portuguese (`pt-BR`) Broadband model | `false` |
| `global.sttModels.ptBrNarrowbandModel.enabled` | Brazilian Portuguese (`pt-BR`) Narrowband model | `false` |
| `global.sttModels.zhCnBroadbandModel.enabled` | Mandarin Chinese (`zh-CN`) Broadband model | `false` |
| `global.sttModels.zhCnNarrowbandModel.enabled` | Mandarin Chinese (`zh-CN`) Narrowband model | `false` |
{: caption="Table 9. Installation of {{site.data.keyword.speechtotextshort}} models"}

## Override values for the {{site.data.keyword.texttospeechshort}} service
{: #speech-override-tts-12}

The following sections describe override values that are specific to the {{site.data.keyword.texttospeechshort}} service.

### Configuring the {{site.data.keyword.texttospeechshort}} runtime
{: #speech-override-tts-runtime-12}

Table 10 describes the configuration values for the {{site.data.keyword.texttospeechshort}} runtime.

| Value | Specifies ... | Default |
|-------|---------------|:-------:|
| `ttsRuntime.groups.ttsRuntimeDefault.resources.dynamicMemory` | Automatic calculation of memory requirements for the {{site.data.keyword.texttospeechshort}} runtime according to the selected voices. | `true` |
| `ttsRuntime.groups.ttsRuntimeDefault.resources.requestsCpu` | Requested CPUs for the {{site.data.keyword.texttospeechshort}} runtime. The minimum value is 4. Each runtime session needs at least 4 CPUs. | `8` |
| `ttsRuntime.groups.ttsRuntimeDefault.resources.requestsMemory` | Memory requirements for the {{site.data.keyword.texttospeechshort}} runtime. When dynamic memory is enabled, this value has no effect. | `22Gi` |
| `global.ttsVoiceMarginalCPU` | {{site.data.keyword.texttospeechshort}} voice marginal CPU used for synthesis. The value is in milli-CPUs. | `400` |
{: caption="Table 10. Configuration of {{site.data.keyword.texttospeechshort}} runtime"}

### Installing {{site.data.keyword.texttospeechshort}} voices
{: #speech-override-tts-voices-12}

You can use the values in Table 11 to specify the voices to install. Installing all voices increases the memory requirements. You are therefore encouraged to install only those voices that you intend to use. By default, the dynamic resource calculation feature automatically computes the exact amount of memory that is required for the selected voices.

You specify the voices to be installed by setting the values in the `speech-override.yaml` file to `true` or `false`. For example, to install the German, French, and Italian voices instead of the US English voices, modify the `global.ttsVoices` values as follows:

```yaml
global:
  ttsVoices:
    enUSMichaelV3Voice:
      enabled: false
    enUSAllisonV3Voice:
      enabled: false
    enUSLisaV3Voice:
      enabled: false
    deDEBirgitV3Voice:
      enabled: true
    deDEDieterV3Voice:
      enabled: true
    deDEErikaV3Voice:
      enabled: true
    frFRReneeV3Voice:
      enabled: true
    itITFrancescaV3Voice:
      enabled: true
```
{: codeblock}

For more information about all available voices, see [Languages and voices](/docs/text-to-speech-data?topic=text-to-speech-data-voices). For information about updating the override file to install ad hoc voices, see [Installing ad hoc models and voices](/docs/text-to-speech-data?topic=text-to-speech-data-speech-cluster-12#speech-cluster-model-install-adhoc-12).

| Value | Installs ... | Default |
|-------|--------------|:-------:|
| `global.ttsVoices.enUSAllisonV3Voice.enabled` | US English (`en-US`) Allison neural voice | `true` |
| `global.ttsVoices.enUSLisaV3Voice.enabled` | US English (`en-US`) Lisa neural voice | `true` |
| `global.ttsVoices.enUSMichaelV3Voice.enabled` | US English (`en-US`) Michael neural voice | `true` |
| `global.ttsVoices.enUSEmilyV3Voice.enabled` | US English (`en-US`) Emily neural voice | `false` |
| `global.ttsVoices.enUSHenryV3Voice.enabled` | US English (`en-US`) Henry neural voice | `false` |
| `global.ttsVoices.enUSKevinV3Voice.enabled` | US English (`en-US`) Kevin neural voice | `false` |
| `global.ttsVoices.enUSOliviaV3Voice.enabled` | US English (`en-US`) Olivia neural voice | `false` |
| `global.ttsVoices.deDEBirgitV3Voice.enabled` | German (`de-DE`) Birgit neural voice | `false` |
| `global.ttsVoices.deDEDieterV3Voice.enabled` | German (`de-DE`) Dieter neural voice | `false` |
| `global.ttsVoices.deDeErikaV3Voice.enabled` | German (`de-DE`) Erika neural voice | `false` |
| `global.ttsVoices.enGBCharlotteV3Voice.enabled` | UK English (`en-GB`) Charlotte neural voice | `false` |
| `global.ttsVoices.enGBJamesV3Voice.enabled` | UK English (`en-GB`) James neural voice | `false` |
| `global.ttsVoices.enGBKateV3Voice.enabled` | UK English (`en-GB`) Kate neural voice | `false` |
| `global.ttsVoices.esESEnriqueV3Voice.enabled` | Spanish (`es-ES`) Enrique neural voice | `false` |
| `global.ttsVoices.esESLauraV3Voice.enabled` | Spanish (`es-ES`) Laura neural voice | `false` |
| `global.ttsVoices.esLASofiaV3Voice.enabled` | Latin American Spanish (`es-LA`) Sofia neural voice | `false` |
| `global.ttsVoices.esUSSofiaV3Voice.enabled` | North American Spanish (`es-US`) Sofia neural voice | `false` |
| `global.ttsVoices.frFRNicolasV3Voice.enabled` | French (`fr-FR`) Nicolas neural voice | `false` |
| `global.ttsVoices.frFRReneeV3Voice.enabled` | French (`fr-FR`) Renee neural voice | `false` |
| `global.ttsVoices.itITFrancescaV3Voice.enabled` | Italian (`it-IT`) Francesca neural voice | `false` |
| `global.ttsVoices.jaJPEmiV3Voice.enabled` | Japanese (`ja-JP`) Emi neural voice | `false` |
| `global.ttsVoices.ptBRIsabelaV3Voice.enabled` | Brazilian Portuguese (`pt-BR`) Isabela neural voice | `false` |
{: caption="Table 11. Installation of {{site.data.keyword.texttospeechshort}} voices"}
