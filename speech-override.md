---

copyright:
  years: 2020
lastupdated: "2020-06-20"

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
{:download: .download}
{:gif: data-image-type='gif'}

# Using the override file
{: #speech-override}

You can use the `speech-override.yaml` file to customize many aspects of your {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} installation. The installation procedure in the IBM Knowledge Center shows an abbreviated example of the `speech-override.yaml` file. But an override file can include many more installation and configuration values.

## The speech-override.yaml file
{: #speech-override-file}

The following example duplicates the `speech-override.yaml` example from [Override values for {{site.data.keyword.watson}} {{site.data.keyword.speechtotextshort}} installation](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/watson/speech-to-text-override.html){: external} and [Override values for {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} installation](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/watson/text-to-speech-override.html){: external}. The sections that follow describe the values you can use to modify and augment the file. You can download a complete copy of the <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/speech-override.yaml" download="speech-override.yaml">speech-override.yaml <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a> file.

```yaml
tags:
  sttAsync: true
  sttCustomization: true
  ttsCustomization: true
  sttRuntime: true
  ttsRuntime: true

affinity: {}

global:
  dockerRegistryPrefix: "cp.icr.io/cp/watson-speech"
  image:
    pullSecret: "docker-pull-{{ .Release.Namespace }}-cp-icr-io-spch-registry-registry"
    pullPolicy: "IfNotPresent"

  datastores:
    minio:
      secretName: "minio"
    postgressql:
      auth:
        authSecretName: "user-provided-postgressql"

  sttModels:
    enUsBroadbandModel:
      enabled: true
    enUsNarrowbandModel:
      enabled: true
    enUsShortFormNarrowbandModel:
      enabled: true

  ttsVoices:
    enUSAllisonV3Voice:
      enabled: true
    enUSLisaV3Voice:
      enabled: true
    enUSMichaelV3Voice:
      enabled: true
```
{: codeblock}

## Override values for both Speech services
{: #speech-override-both}

The following sections describe override values that apply to both Speech services.

### Installing Speech services components
{: #speech-override-components}

The following five main components provide the base {{site.data.keyword.speechtotextshort}} and  {{site.data.keyword.texttospeechshort}} functionality. You can set these tags in the `speech-override.yaml` file to enable or disable the installation of each of the components.

By default, all of the components are enabled, but you can enable or disable them separately.

-   To install {{site.data.keyword.speechtotextshort}} only, set `ttsRuntime` and `ttsCustomization` to `false`.
-   To install  {{site.data.keyword.texttospeechshort}} only, set `sttRuntime`, `sttCustomization`, and `sttAsync` to `false`.
-   To install both {{site.data.keyword.speechtotextshort}} and  {{site.data.keyword.texttospeechshort}} without enabling customization, set `sttCustomization` and `ttsCustomization` to `false`.

Table 1 describes the top-level Speech components that you can install.

<table>
  <caption>Table 1. Installation of Speech services components</caption>
  <tr>
    <th>
      Value
    </th>
    <th>
      Installs ...
    </th>
    <th style="text-align:center">
      Default
    </th>
  </tr>
  <tr>
    <td>
      `tags.sttRuntime`
    </td>
    <td>
      {{site.data.keyword.speechtotextshort}} runtime component, the base
      component for speech recognition. This value enables the `/v1/recognize`
      interfaces (synchronous HTTP and WebSocket). Enabling any other
      {{site.data.keyword.speechtotextshort}} component automatically enables
      the {{site.data.keyword.speechtotextshort}} runtime component. For more
      information, see
      [The synchronous HTTP interface](/docs/speech-to-text-data?topic=speech-to-text-data-http)
      and [The WebSocket interface](/docs/speech-to-text-data?topic=speech-to-text-data-websockets).
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `tags.sttAsync`
    </td>
    <td>
      {{site.data.keyword.speechtotextshort}} asynchronous HTTP component.
      This value enables the `/v1/recognitions` interface.
      For more information, see
      [The asynchronous HTTP interface](/docs/speech-to-text-data?topic=speech-to-text-data-async).
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `tags.sttCustomization`
    </td>
    <td>
      {{site.data.keyword.speechtotextshort}} customization component. This
      value enables the `/v1/customizations` and `/v1/acoustic_customizations`
      interfaces for language model and acoustic model customization. Enabling
      it also enables the {{site.data.keyword.speechtotextshort}} runtime
      component if `tags.sttRuntime=false`. For more information, see
      [The customization interface](/docs/speech-to-text-data?topic=speech-to-text-data-customization).
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `tags.ttsRuntime`
    </td>
    <td>
      {{site.data.keyword.texttospeechshort}} runtime component, the base
      component for speech synthesis. This value enables the `/v1/synthesize`
      interfaces (HTTP and WebSocket). Enabling any other
      {{site.data.keyword.texttospeechshort}} component automatically enables
      the {{site.data.keyword.texttospeechshort}} runtime component. For more
      information, see [The HTTP interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingHTTP)
      and [The WebSocket interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `tags.ttsCustomization`
    </td>
    <td>
      {{site.data.keyword.texttospeechshort}} customization component.
      This value enables the `/v1/customizations` interface for voice
      model customization. Enabling it also enables the
      {{site.data.keyword.texttospeechshort}} runtime component if
      `tags.sttRuntime=false`. For more information, see
      [Understanding customization](/docs/text-to-speech-data?topic=text-to-speech-data-customIntro).
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
</table>

### Configuring datastores
{: #speech-override-datastores}

Table 2 describes the values you can specify to configure the datastores for your installation. For more information about the MinIO and PostgreSQL datastores, see [Managing datastores](/docs/text-to-speech-data?topic=text-to-speech-data-speech-datastores) and [Scaling up your installation](/docs/text-to-speech-data?topic=text-to-speech-data-speech-scaling).

<table>
  <caption>Table 2. Configuration of datastores</caption>
  <tr>
    <th>
      Value
    </th>
    <th>
      Specifies ...
    </th>
    <th style="text-align:center">
      Default
    </th>
  </tr>
  <tr>
    <td>
      `external.minio.mode`
    </td>
    <td>
      MinIO server mode (`standalone` or `distributed`).
    </td>
    <td style="text-align:center">
      `distributed`
    </td>
  </tr>
  <tr>
    <td>
      `external.minio.persistence.size`
    </td>
    <td>
      Size of persistent volume claim (PVC) for MinIO.
    </td>
    <td style="text-align:center">
      `100Gi`
    </td>
  </tr>
  <tr>
    <td>
      `external.minio.replicas`
    </td>
    <td>
      Number of nodes (applicable only for MinIO distributed mode).
      Must be `4 <= x <= 32`.
    </td>
    <td style="text-align:center">
      `4`
    </td>
  </tr>
  <tr>
    <td>
      `external.minio.minioAccessSecret`
    </td>
    <td>
      A secrets object that contains base64-encoded `accesskey` (5 - 20
      characters) and `secretkey` (8 - 40 characters) values. The keys are
      used to access the MinIO Object Server securely. You need to create the
      secrets object in the same namespace in which you deploy the services.
    </td>
    <td style="text-align:center">
      `minio`
    </td>
  </tr>
  <tr>
    <td>
      `global.datastores.minio.secretName`
    </td>
    <td>
      Name of the secrets object that contains the MinIO secrets that are
      needed to access the datastore securely.
    </td>
    <td style="text-align:center">
      `minio`
    </td>
  </tr>
  <tr>
    <td>
      `global.datastores.postgressql.auth.authSecretName`
    </td>
    <td>
      Name of the secrets object that contains the PostgresSQL credentials
      that are needed to access the datastore securely.
    </td>
    <td style="text-align:center">
      `user-provided-postgressql`
    </td>
  </tr>
  <tr>
    <td>
      `postgressql.auth.authSecretName`
    </td>
    <td>
      Name of the secrets object that contains the PostgresSQL credentials
      that are needed to access the datastore securely.
    </td>
    <td style="text-align:center">
      `user-provided-postgressql`
    </td>
  </tr>
</table>

### Specifying dynamic resource calculation
{: #speech-override-dynamic}

The {{site.data.keyword.speechtotextshort}} runtime, {{site.data.keyword.texttospeechshort}} runtime, and {{site.data.keyword.speechtotextshort}} customization AM patcher support dynamic memory resource calculation. The calculation is performed automatically based on the selected number of CPUs and the selected models and voices.

Dynamic resource calculation is enabled by default. You can modify this behavior by setting the values in Table 3 to `true` or `false` in the root of the override file. If you set any of these values to `false`, you must specify the required memory yourself.

Disabling dynamic resource allocation is not recommended and can cause undesired service behavior.
{: important}

<table>
  <caption>Table 3. Configuration of dynamic resource calculation</caption>
  <tr>
    <th>
      Value
    </th>
    <th>
      Enables ...
    </th>
    <th style="text-align:center">
      Default
    </th>
  </tr>
  <tr>
    <td>
      `sttRuntime.groups.sttRuntimeDefault.resources.dynamicMemory`
    </td>
    <td>
      Dynamic resource calculation for the
      {{site.data.keyword.speechtotextshort}} runtime component.
    </td>

    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `ttsRuntime.groups.ttsRuntimeDefault.resources.dynamicMemory`
    </td>
    <td>
      Dynamic resource calculation for the
      {{site.data.keyword.texttospeechshort}} runtime component.
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `sttAMPatcher.groups.sttAMPatcher.resources.dynamicMemory`
    </td>
    <td>
      Dynamic resource calculation for the
      {{site.data.keyword.speechtotextshort}} customization AM patcher
      component.
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
</table>

### Specifying node affinity
{: #speech-override-affinity}

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
{: #speech-override-anonymize}

You can anonymize your log and audio data for increased user privacy. Use the values in Table 4 to anonymize data that is stored by the different components. You can also disable the temporary storing of payload data in the running container. For more information, see [Disabling storage of user data](/docs/text-to-speech-data?topic=text-to-speech-data-speech-cluster#speech-cluster-customer-data).

<table>
  <caption>Table 4. Anonymization of logs and audio data</caption>
  <tr>
    <th>
      Value
    </th>
    <th>
      Anonymizes ...
    </th>
    <th style="text-align:center">
      Default
    </th>
  </tr>
  <tr>
    <td>
      `sttRuntime.anonymizeLogs`
    </td>
    <td>
      {{site.data.keyword.speechtotextshort}} runtime logs and audio data.
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `ttsRuntime.anonymizeLogs`
    </td>
    <td>
      {{site.data.keyword.texttospeechshort}} runtime logs and audio data.
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `sttAMPatcher.anonymizeLogs`
    </td>
    <td>
      {{site.data.keyword.speechtotextshort}} customization acoustic model
      (AM) patcher runtime logs and audio data.
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
</table>

## Override values for the {{site.data.keyword.speechtotextshort}} service
{: #speech-override-stt}

The following sections describe override values that are specific to the {{site.data.keyword.speechtotextshort}} service.

### Configuring the {{site.data.keyword.speechtotextshort}} runtime
{: #speech-override-stt-runtime}

Table 5 describes the configuration values for the {{site.data.keyword.speechtotextshort}} runtime.

<table>
  <caption>Table 5. Configuration of {{site.data.keyword.speechtotextshort}} runtime</caption>
  <tr>
    <th>
      Value
    </th>
    <th>
     Specifies ...
    </th>
    <th style="text-align:center">
      Default
    </th>
  </tr>
  <tr>
    <td>
      `sttRuntime.groups.sttRuntimeDefault.resources.dynamicMemory`
    </td>
    <td>
      Automatic calculation of the memory requirements for the
      {{site.data.keyword.speechtotextshort}} runtime according to the
      selected models.
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `sttRuntime.groups.sttRuntimeDefault.resources.requestsCpu`
    </td>
    <td>
      Requested CPUs for the {{site.data.keyword.speechtotextshort}} runtime.
      The minimum value is 4. Each runtime session needs at least 4 CPUs.
    </td>
    <td style="text-align:center">
      `8`
    </td>
  </tr>
  <tr>
    <td>
      `sttRuntime.groups.sttRuntimeDefault.resources.requestsMemory`
    </td>
    <td>
      Memory requirements for the {{site.data.keyword.speechtotextshort}}
      runtime. When dynamic memory is enabled, this value has no effect.
    </td>
    <td style="text-align:center">
      `22Gi`
    </td>
  </tr>
</table>

### Configuring the {{site.data.keyword.speechtotextshort}} customization AM patcher
{: #speech-override-stt-AMpatcher}

Table 6 describes the configuration values for the {{site.data.keyword.speechtotextshort}} customization AM patcher.

<table>
  <caption>Table 6. Configuration of {{site.data.keyword.speechtotextshort}} customization AM patcher</caption>
  <tr>
    <th>
      Value
    </th>
    <th>
      Specifies ...
    </th>
    <th style="text-align:center">
      Default
    </th>
  </tr>
  <tr>
    <td>
      `sttAMPatcher.groups.sttAMPatcher.resources.dynamicMemory`
    </td>
    <td>
      Automatic calculation of the memory requirements for the
      {{site.data.keyword.speechtotextshort}} customization AM patcher
      according to the selected models.
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `sttAMPatcher.groups.sttAMPatcher.resources.requestsCpu`
    </td>
    <td>
      Requested CPUs for the {{site.data.keyword.speechtotextshort}}
      customization AM patcher. The minimum value is 4. Each customization
      session needs at least 4 CPUs.
    </td>
    <td style="text-align:center">
      `8`
    </td>
  </tr>
  <tr>
    <td>
      `sttAMPatcher.groups.sttAMPatcher.resources.requestsMemory`
    </td>
    <td>
      Memory requirements for the {{site.data.keyword.speechtotextshort}}
      customization AM patcher. The amount of memory depends on the number
      of CPUs. The size can be calculated as the number of CPUs * 3 GB.
    </td>
    <td style="text-align:center">
      `22Gi`
    </td>
  </tr>
  <tr>
    <td>
      `sttAMPatcher.groups.sttAMPatcher.resources.threads`
    </td>
    <td>
      Number of parallel-processing threads for the
      {{site.data.keyword.speechtotextshort}} customization AM patcher.
      Note that fewer threads means longer training time.
    </td>
    <td style="text-align:center">
      `4`
    </td>
  </tr>
</table>

### Installing {{site.data.keyword.speechtotextshort}} models
{: #speech-override-stt-models}

You can use the values in Table 7 to specify the language models to install. Installing all models substantially increases the memory requirements. You are therefore strongly encouraged to install only those models and voices that you intend to use. By default, the dynamic resource calculation feature automatically computes the exact amount of memory that is required for the selected models.

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

For more information about all available models, see [Languages and models](/docs/speech-to-text-data?topic=speech-to-text-data-models). For information about updating the override file to install ad hoc models, see [Installing ad hoc models and voices](/docs/text-to-speech-data?topic=text-to-speech-data-speech-cluster#speech-cluster-model-install-adhoc).

<table>
  <caption>Table 7. Installation of {{site.data.keyword.speechtotextshort}} models</caption>
  <tr>
    <th>
      Value
    </th>
    <th>
      Installs ...
    </th>
    <th style="text-align:center">
      Default
    </th>
  </tr>
  <tr>
    <td>
      `global.sttModels.enUsBroadbandModel.enabled`
    </td>
    <td>
      US English (`en-US`) Broadband model
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.enUsNarrowbandModel.enabled`
    </td>
    <td>
      US English (`en-US`) Narrowband model
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.enUsShortFormNarrowbandModel.enabled`
    </td>
    <td>
      US English (`en-US`) Short-Form Narrowband model
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.arArBroadbandModel.enabled`
    </td>
    <td>
      Modern Standard Arabic (`ar-AR`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.enGbBroadbandModel.enabled`
    </td>
    <td>
      UK English (`en-GB`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.enGbNarrowbandModel.enabled`
    </td>
    <td>
      UK English (`en-GB`) Narrowband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.esEsBroadbandModel.enabled`
    </td>
    <td>
      Spanish (`es-ES`, `es-AR`, `es-CL`, `es-CO`, `es-MX`, and `es-PE`)
      Broadband models
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.esEsNarrowbandModel.enabled`
    </td>
    <td>
      Spanish (`es-ES`, `es-AR`, `es-CL`, `es-CO`, `es-MX`, and `es-PE`)
      Narrowband models
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.frFrBroadbandModel.enabled`
    </td>
    <td>
      French (`fr-FR`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.frFrNarrowbandModel.enabled`
    </td>
    <td>
      French (`fr-FR`) Narrowband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.deDeBroadbandModel.enabled`
    </td>
    <td>
      German (`de-DE`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.deDeNarrowbandModel.enabled`
    </td>
    <td>
      German (`de-DE`) Narrowband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.itItBroadbandModel.enabled`
    </td>
    <td>
      Italian (`it-IT`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.itItNarrowbandModel.enabled`
    </td>
    <td>
      Italian (`it-IT`) Narrowband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.jaJpBroadbandModel.enabled`
    </td>
    <td>
      Japanese (`ja-JP`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.jaJpNarrowbandModel.enabled`
    </td>
    <td>
      Japanese (`ja-JP`) Narrowband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.koKrBroadbandModel.enabled`
    </td>
    <td>
      Korean (`ko-KR`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.koKrNarrowbandModel.enabled`
    </td>
    <td>
      Korean (`ko-KR`) Narrowband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.nlNlBroadbandModel.enabled`
    </td>
    <td>
      Dutch (`nl-NL`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.nlNlNarrowbandModel.enabled`
    </td>
    <td>
      Dutch (`nl-NL`) Narrowband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.ptBrBroadbandModel.enabled`
    </td>
    <td>
      Brazilian Portuguese (`pt-BR`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.ptBrNarrowbandModel.enabled`
    </td>
    <td>
      Brazilian Portuguese (`pt-BR`) Narrowband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.zhCnBroadbandModel.enabled`
    </td>
    <td>
      Mandarin Chinese (`zh-CN`) Broadband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.sttModels.zhCnNarrowbandModel.enabled`
    </td>
    <td>
      Mandarin Chinese (`zh-CN`) Narrowband model
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
</table>

## Override values for the {{site.data.keyword.texttospeechshort}} service
{: #speech-override-tts}

The following sections describe override values that are specific to the {{site.data.keyword.texttospeechshort}} service.

### Configuring the {{site.data.keyword.texttospeechshort}} runtime
{: #speech-override-tts-runtime}

Table 8 describes the configuration values for the {{site.data.keyword.texttospeechshort}} runtime.

<table>
  <caption>Table 8. Configuration of {{site.data.keyword.texttospeechshort}} runtime</caption>
  <tr>
    <th>
      Value
    </th>
    <th>
      Specifies ...
    </th>
    <th style="text-align:center">
      Default
    </th>
  </tr>
  <tr>
    <td>
      `ttsRuntime.groups.ttsRuntimeDefault.resources.dynamicMemory`
    </td>
    <td>
      Automatic calculation of memory requirements for the
      {{site.data.keyword.texttospeechshort}} runtime according to the
      selected voices.
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `ttsRuntime.groups.ttsRuntimeDefault.resources.requestsCpu`
    </td>
    <td>
      Requested CPUs for the {{site.data.keyword.texttospeechshort}} runtime.
      The minimum value is 4. Each runtime session needs at least 4 CPUs.
    </td>
    <td style="text-align:center">
      `8`
    </td>
  </tr>
  <tr>
    <td>
      `ttsRuntime.groups.ttsRuntimeDefault.resources.requestsMemory`
    </td>
    <td>
      Memory requirements for the {{site.data.keyword.texttospeechshort}}
      runtime. When dynamic memory is enabled, this value has no effect.
    </td>
    <td style="text-align:center">
      `22Gi`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoiceMarginalCPU`
    </td>
    <td>
      {{site.data.keyword.texttospeechshort}} voice marginal CPU used for
      synthesis. The value is in milli-CPUs.
    </td>
    <td style="text-align:center">
      `400`
    </td>
  </tr>
</table>

### Installing {{site.data.keyword.texttospeechshort}} voices
{: #speech-override-tts-voices}

You can use the values in Table 9 to specify the voices to install. Installing all voices increases the memory requirements. You are therefore encouraged to install only those voices that you intend to use. By default, the dynamic resource calculation feature automatically computes the exact amount of memory that is required for the selected voices.

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

For more information about all available voices, see [Languages and voices](/docs/text-to-speech-data?topic=text-to-speech-data-voices). For information about updating the override file to install ad hoc voices, see [Installing ad hoc models and voices](/docs/text-to-speech-data?topic=text-to-speech-data-speech-cluster#speech-cluster-model-install-adhoc).

<table>
  <caption>Table 9. Installation of {{site.data.keyword.texttospeechshort}} voices</caption>
  <tr>
    <th>
      Value
    </th>
    <th>
      Installs ...
    </th>
    <th style="text-align:center">
      Default
    </th>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.enUSAllisonV3Voice.enabled`
    </td>
    <td>
      US English (`en-US`) Allison neural voice
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.enUSLisaV3Voice.enabled`
    </td>
    <td>
      US English (`en-US`) Lisa neural voice
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.enUSMichaelV3Voice.enabled`
    </td>
    <td>
      US English (`en-US`) Michael neural voice
    </td>
    <td style="text-align:center">
      `True`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.enUSEmilyV3Voice.enabled`
    </td>
    <td>
      US English (`en-US`) Emily neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.enUSHenryV3Voice.enabled`
    </td>
    <td>
      US English (`en-US`) Henry neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.enUSKevinV3Voice.enabled`
    </td>
    <td>
      US English (`en-US`) Kevin neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.enUSOliviaV3Voice.enabled`
    </td>
    <td>
      US English (`en-US`) Olivia neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.deDEBirgitV3Voice.enabled`
    </td>
    <td>
      German (`de-DE`) Birgit neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.deDEDieterV3Voice.enabled`
    </td>
    <td>
      German (`de-DE`) Dieter neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.deDeErikaV3Voice.enabled`
    </td>
    <td>
      German (`de-DE`) Erika neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.enGBKateV3Voice.enabled`
    </td>
    <td>
      UK English (`en-GB`) Kate neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.esESEnriqueV3Voice.enabled`
    </td>
    <td>
      Spanish (`es-ES`) Enrique neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.esESLauraV3Voice.enabled`
    </td>
    <td>
      Spanish (`es-ES`) Laura neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.esLASofiaV3Voice.enabled`
    </td>
    <td>
      Latin American Spanish (`es-LA`) Sofia neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.esUSSofiaV3Voice.enabled`
    </td>
    <td>
      North American Spanish (`es-US`) Sofia neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.frFRReneeV3Voice.enabled`
    </td>
    <td>
      French (`fr-FR`) Renee neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.itITFrancescaV3Voice.enabled`
    </td>
    <td>
      Italian (`it-IT`) Francesca neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.jaJPEmiV3Voice.enabled`
    </td>
    <td>
      Japanese (`ja-JP`) Emi neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
  <tr>
    <td>
      `global.ttsVoices.ptBRIsabelaV3Voice.enabled`
    </td>
    <td>
      Brazilian Portuguese (`pt-BR`) Isabela neural voice
    </td>
    <td style="text-align:center">
      `False`
    </td>
  </tr>
</table>
