---

copyright:
  years: 2018, 2019
lastupdated: "2019-11-20"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:gif: data-image-type='gif'}

# Installing the Watson Text to Speech add-on
{: #stt-installing}

You can install the {{site.data.keyword.texttospeechdatafull}} add-on on top of {{site.data.keyword.icp4dfull}}, with or without Red Hat OpenShift.
{: shortdesc}

## Introduction
{: #stt-intro}

This document contains installation instructions for both {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} solutions.

{{site.data.keyword.speechtotextshort}} (STT) provides speech recognition capabilities for your solutions. The service uses machine learning to combine knowledge of grammar, language structure, and the composition of audio and voice signals to accurately transcribe the human voice. It continuously updates and refines its transcription as it receives more speech.

{{site.data.keyword.texttospeechshort}} (TTS) converts written text to natural-sounding speech to provide speech-synthesis capabilities for applications. It gives you the freedom to customize your own preferred speech in different languages.

## Chart details
{: #chart-details}

This chart can be used to install a single instance of both the *STT* and *TTS* solutions. The solutions can be installed separately; however, if both are installed together they share their datastores for a more efficient utilization of resources and simplified support.

## Prerequisites
{: #prereqs}

  - IBM Cloud Pak for Data v2.1.0.1 or v2.5
  - Kubernetes v1.12.4 or later
  - Helm v2.9.1 or later

Before installing the Speech Services solution, you must install and configure [`helm`](https://helm.sh/docs/using_helm/#installing-the-helm-client) and [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html).

## Selecting the components to install
{: #select-components}

This chart can be used to install both the *STT* and *TTS* solutions. The following tags, which are defined in the `values.yaml` file, can be used to enable the installation of each of the different components shipped in this solution:

```yaml
tags:
  sttAsync: true
  sttCustomization: true
  ttsCustomization: true
  sttRuntime: true
  ttsRuntime: true
```

- `sttAsync` enables the installation of the asynchronous API to access the STT service, which corresponds to the `/recognitions` API endpoints.
- `sttCustomization` enables the installation of the STT customization functionality, which lets you customize the STT base models for improved accuracy and corresponds to the `/customizations` API endpoints.
- `ttsCustomization` enables the installation of the TTS customization functionality, which lets you customize the TTS base voices for improved voice quality and corresponds to the `/customizations` API endpoints.
- `sttRuntime` enables the installation of the core STT functionality, which lets you convert speech into text by using the `/recognize` endpoint. Note that this component is installed if any of the `sttRuntime`, `sttCustomization`, or `sttAsync` tags are set to `true`.
- `ttsRuntime` enables the installation of the core TTS functionality, which lets you convert text into speech by using the `/synthesize` endpoint.  Note that this component is installed if either the `ttsRuntime` or `ttsCustomization` tags are set to `true`.

By default all the components are enabled, but each of them can be disabled separately. If you want to install *STT* only, you need to set `ttsRuntime` and `ttsCustomization` to `false`. Similarly, if you want to install *TTS* only, you need to set `sttRuntime`, `sttCustomization`, and `sttAsync` to `false`. For example, if you want to install *STT* and *TTS* but do not want customization capabilities, then you need to set `sttCustomization` and `ttsCustomization` to `false`.

## Namespace
{: #namespace}

The first step consists of creating the Kubernetes namespace where the solution is to be installed. The following examples shows how to create the namespace, which in this case is named `speech-services`. You can use a different name for the namespace.

Copy the following YAML to a file, then run the `kubectl` command that follows the YAML. In the command, replace `{namespace-file}` with the name of the file to which you copied the YAML.

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: speech-services
```

```sh
kubectl create -f {namespace-file}
```

## Configuring Minio object storage
{: #config-minio}

Minio object storage is used for storing persistent data needed by speech service components.

### Secrets
{: #minio-secrets}

Before you install *STT* or *TTS*, you need to provide a secret object that is used by Minio itself and by other service components that interact with Minio. This secret contains the security keys to access Minio.

The secret must contain the items `accesskey` (5 - 20 characters) and `secretkey` (8 - 40 characters) in `base64` encoding. Therefore, before creating the secret, you need to perform the `base64` encoding.

The following commands encode the `accesskey` and `secretkey` in `base64`. **Important:** For security reasons, you are strongly encouraged to create an `accesskey` and a `secretkey` that are different from the sample keys (`admin` and `admin1234`) that are shown in the examples.

```sh
echo -n "admin" | base64
YWRtaW4=

echo -n "admin1234" | base64
YWRtaW4xMjM0
```

Create a file named `minio.yaml` with the following secret object definition, then run the `kubectl` command that follows the file contents.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: minio
type: Opaque
data:
  accesskey: YWRtaW4=
  secretkey: YWRtaW4xMjM0
```

```sh
kubectl create -f minio.yaml
```

### Setting up data persistence
{: #minio-persistence}

Minio requires a storage backend to store persistent data. For *STT* and *TTS*, Minio can use any one of the following storage backends:

  - [Portworx](#use-portworx)
  - [GlusterFS](#use-minio-glusterfs)
  - [NFS](#use-minio-nfs)

#### Using Portworx as a storage solution
{: #use-portworx}

To configure the installation to use [Portworx](https://portworx.com/) persistent volumes, a Portworx k8 Storage Class needs to exist in the cluster. A dynamic provisioner is then enabled, which can be used to dynamically provision new volumes. See [the Portworx documentation](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/kubernetes-storage-101/volumes/#storageclass){: external} for more details.

After the Storage Class is available, its name needs to be passed to Minio, PostgreSQL and RabbitMQ, which is shown in the following list. The list assumes that `portworx-sc` is the name of the Storage Class. Additionally, dynamic provisioning needs to be enabled. These are the values that need to be passed at installation time:

- Minio: `external.minio.persistence.useDynamicProvisioning: true` and `external.minio.persistence.storageClass: portworx-sc`.
- PostgreSQL: `postgressql.persistence.useDynamicProvisioning: true` and `postgressql.persistence.storageClassName: portworx-sc`.
- RabbitMQ: `rabbitmqHA.persistentVolume.useDynamicProvisioning: true` and `rabbitmqHA.persistentVolume.storageClassName: portworx-sc`.

#### Using Minio on GlusterFS as a storage solution
{: #use-minio-glusterfs}

To use Minio you need to have a running GlusterFS server and create a storage class name `oketi-gluster`. For information about installing GlusterFS under IBM Cloud Private, see [Configuring GlusterFS](https://www.ibm.com/support/knowledgecenter/en/SSBS6K_3.1.2/manage_cluster/configure_glusterfs.html). It is possible that you created the `oketi-gluster` storage class during IBM Cloud Private installation. If not, create it as follows:

```sh
cat > oketi-gluster.yaml << EOF
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: oketi-gluster
  parameters:
    nodes: |
      [
        { "Hostname":"HOST", "IP":"$GLUSTER_SERVER", "Path":"$GLUSTER_DIR"},
      ]
    volumeType: glusterfs
  provisioner: oketi
  reclaimPolicy: Retain
  volumeBindingMode: Immediate
EOF
```

where `$GLUSTER_SERVER` is the address of the GlusterFS server and `$GLUSTER_DIR` is the root of the GlusterFS directory. After modifying and saving the file as appropriate, run  `kubectl apply -f oketi-gluster.yaml`.

The GlusterFS server must be installed with sufficient space size. Size calculation is described in [Storage size calculation guidelines](#minio-storage-size-calculations).

#### Using Minio on NFS as a storage solution
{: #use-minio-nfs}

If the NFS server uses a persistent volume provisioner, then it is necessary to create a storage class that Minio can leverage to create the persistent volumes automatically during installation.

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: oketi-nfs
parameters:
  nodes: |
    [
      { "Hostname":"HOST", "IP":"$NFS_SERVER", "Path":"$NFS_DIR"}
    ]
  volumeType: nfs
provisioner: $PROVISIONER       # for example oketi
reclaimPolicy: Retain
volumeBindingMode: Immediate
```

If the NFS server does not use a provisioner, disable automatic provisioning by setting the value `external.minio.peristence.useDynamicProvisioning` to `false`. Create the the persistent volumes explicitly before performing the installation as described in the following sections. Note that it is necessary to create a persistent volume for each Minio replica. The directories where the persistent volumes are mounted must have non-root access so the Minio pods can write to them. Permissions can be changed by running the `chmod` command from the cluster nodes.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: minio-nfs-0
spec:
  capacity:
    storage: $CAPACITY      # for example: 100Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy:  
  nfs:
    server: $NFS_SERVER     # for example: 9.46.65.38
    path: $NFS_DIR          # for example: /NFSDataStore/speech_minio/dir0
```

### Mode of operation
{: #minio-mode-of-operation}

By default, Minio operates in `distributed` mode, which means that Minio is scheduled to run multiple instance on every worker node to assure storage high availability.

To use HA optimally, you must specify an appropriate number of replicas. Set the number of replicas for distributed mode by running `external.minio.replicas={number-of-cluster-nodes}`, where `{number-of-cluster-nodes}` is `4 <= x <= 32`. The default value is `4` replicas.

Minio also operates in `standalone` mode, which means that only one instance of Minio runs on an arbitrary worker node and its failure means that the service becomes available until a new instance is running and healthy. This option is sufficient for testing purposes but not for production.

If you want to run Minio in `standalone` mode, you can do it by setting the value `external.minio.mode=standalone`. In this case you do not have to set the `external.minio.replicas` value.

### Storage size calculation guidelines
{: #minio-storage-size-calculations}

Object storage is used for storing binary data from the following sources:

  - Base models (for example `en_US-NarrowbandModel`)

    On average, base models are each `1.5 GB`. Because models are updated regularly, you need to multiply that amount by three to make room for at least three different versions of each model.

  - Customization data (audio files and training snapshots)

    The storage required for customization data depends on how many hours of audio you use for training your custom models. On average, one hour of audio data needs `0.5 GB` of storage space. You can have multiple customizations, so you must factor in additional space.

  - Audio files from recognition jobs that are processed asynchronously, in case they need to be queued.

    The storage required for asynchronous jobs depends on the use case. If you plan to submit large batches of audio files, expect the service to queue some jobs temporarily. This means that some audio files are held temporarily in binary storage. The amount of storage required for this purpose does not exceed the size of the largest batch of jobs that you plan to submit in parallel.

A few examples of how to calculate storage size follow. The unit in the following examples is `GB`.

  -   6 models, 3 versions, 50 hours audio = `6 * 1.5 * 3 + 50 * 0.5 = 52`
  -   2 models, 3 versions, 20 hours audio = `2 * 1.5 * 3 + 20 * 0.5 = 19`

The default storage size, `100 GB`, is a minimal starting point and is typically enough for operations with two to six models and about 50 hours of audio for the purpose of training custom models. That said, it is always a good idea to be generous in anticipation of future storage needs.

## Configuring the PostgreSQL and RabbitMQ installations
{: #stt-config-postgresql-rabbitmq}

PostgreSQL and RabbitMQ must be configured as follows for the *STT* and *TTS* solutions.

### Setting access credentials for PostgreSQL
{: #stt-access-creds-postgresql}

The Postgres chart reads the credentials to access the Postgres database from the following secret file, which needs to be created before installing the chart. You need to set the attribute `data.pg_su_password` to the Postgres password that you want (`base64` encoded). You also need to set the attribute `pg_repl_password`, which is the replication password and is also `base64` encoded, to the value you want.

```yaml
apiVersion: v1
data:
  pg_repl_password: cmVwbHVzZXI=
  pg_su_password: c3RvbG9u
kind: Secret
metadata:
  name: user-provided-postgressql # this name can be anything you choose
type: Opaque
```

To create the secret object, run the `kubectl create -f {secrets_file}` command.

Finally, when installing the chart you need to set the following two values to the name of the previously created secret (`user-provided-postgressql`): `global.datastores.postgressql.auth.authSecretName` and `postgressql.auth.authSecretName`.

If you do not create the secret object, the installation creates a secret object that contains randomly generated passwords when the Helm chart is installed. For security reasons, you need to change the automatically generated passwords when the deployment is complete.

### Creating Local Persistent Volumes to persist data
{: #stt-create-lpvs}

If one or more of the *STT* customization, *TTS* customization, or *STT* async components are included in the installation, as described in [Selecting the components to install](#select-components), an instance of the PostgreSQL database is installed. Additionally, if the *STT* async component is included in the installation, an instance of the RabbitMQ datastore is installed. The datastores are stateful and need to leverage Kubernetes persistent volumes to persist their data.

PostgreSQL and RabbitMQ require the availability of Kubernetes Local Persistent Volumes, which must be created before you install the chart. The volumes are used to persist the data used by the datastores so if a container restarts it can reattach to the original data. Given that both PostgreSQL and RabbitMQ are configured by default for high availability (HA) with three replicas, a minimum of three volumes need to be installed for each of the datastores.

You can create the Local Persistent Volumes by using the `createLocalPVs.sh` script provided within this chart, as explained in the installation instructions. You can also manually create Local Persistent Volumes by using a template such as the following for each persistent volume that need to be created.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: {name}
spec:
  capacity:
    storage: {size}Gi
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: local-storage-local
  local:
    path: {path}
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - {node}
```

where:
  - `{name}` is the name of the Persistent Volume (PV) to be created, and needs to be unique.
  - `{size}` is the disk space that is allocated for the persistent volume.
  - `{path}` is the path in the host machine where the persistent volume is created; for example, `/mnt/local-storage/storage/pv_1`. Note that the permissions of this directory need to be open enough to permit non-root access; otherwise, pods running as non-root are unable to mount the volume in the directory.
  - `{node}` is the Kubernetes *worker* node where the Local Volume is to be created. You can list the available nodes in your cluster by running `kubectl get nodes`.

Given that PostgreSQL and RabbitMQ pods are scheduled in the worker nodes where the PVs are created, the PVs need to be created in different nodes so if a node goes down there are still at least two healthy replicas running. Recall that a minimum of three replicas are needed for high availability.

## Required resources
{: #stt-required-resources}

In addition to the general requirements listed in [Pre-installation tasks](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/preinstall-overview.html), *STT* and *TTS* have their own requirements:

  - `x86_64` is the only architecture supported at this time.
  - If you need a highly available installation, a minimum of three worker nodes are needed for the installation.
  - The resources required for the installation, in terms of CPUs and memory, depend on the configuration that you select. There are two typical installation configurations:
    - The **development configuration**, which is the configuration that is used in the default installation, has a minimal footprint and is meant for development purposes and as a proof of concept. It can handle several concurrent recognition sessions only and it is not highly available because some of the core component have no redundancy (single replica).
    - The **production configuration** is a highly available solution that is intended to run production workloads. This configuration can be achieved by scaling up the **development configuration** after installation, as described in the following section.

### Scaling up the **development configuration** to obtain a **production configuration**
{: #stt-scale-dev-to-prod}

While the default installation of the solution comes with the **development configuration**, you can update it to the **production configuration** by scaling up the number of pods and replicas of the deployment objects after installing the solution. How much to scale up each of the components depends on the degree of concurrency you need, and is limited by the amount of hardware resources available in your Kubernetes cluster/namespace.

#### Scaling up the PostgreSQL and RabbitMQ datastores
{: #stt-scale-postgresql-rabbitmq}

By default both PostgreSQL and RabbitMQ are installed with three replicas for high availability reasons. Each replica is typically scheduled within a different Kubernetes worker node if resources permit. Before performing the installation, you can configure the number of replicas and the CPU and memory resources for each replica by using Helm values. For more information, see [Options](#options).

You can also scale up the datastores on an already running solution by changing the number of replicas in the Deployment or StatefulSet objects. For example, you can scale up RabbitMQ as follows:

  1. Edit the StatefulSet object by running `kubectl edit statefulsets {release}-ibm-rabbitmq`.
  1. Change the value of the `spec.replicas:` attribute.
  1. Save and close the StatefulSet object.

PostgreSQL includes two deployment objects (`{release}-ibm-postgresql-proxy` and `{release}-ibm-postgresql-sentinel`) and a StatefulSet (`ibm-wc-ibm-postgresql-keeper`). The deployment objects can be scaled up by running `kubectl scale --replicas={n} {deployment_object}`, where `{n}` is the new number of replicas; for example, `kubectl scale --replicas=3 deployment ibm-wc-ibm-postgresql-proxy`. The StatefulSet object can be scaled up by following the process described previously for PostgreSQL.  

Note that a sufficient number of Persistent Local Volumes need to be created before scaling up the number of replicas (in the case of the StatefulSets) so the newly created pods can mount their volumes.

#### Scaling up the rest of the solution
{: #stt-scale-solution}

You can learn about the list of deployments (Kubernetes `Deployment` objects) by running the `kubectl get deployment` command. You can then scale up the number of pods on each of the deployment objects to match the number of pods in the production configuration, as shown in the following table. You can do this by using the following command: `kubectl scale --replicas={n} deployment {deployment_object}`, where `{n}` is the desired number of replicas for the given deployment (`{deployment_object}`).

| Deployment              | Default number of replicas |
|-------------------------|-------------------|
| `{release-name}-speech-to-text-stt-runtime`          |  1 |
| `{release-name}-speech-to-text-stt-customization`    |  1 |
| `{release-name}-speech-to-text-stt-am-patcher`       |  1 |
| `{release-name}-speech-to-text-stt-async`            |  1 |
| `{release-name}-speech-to-text-gdpr-data-deletion`   |  1 |
| `{release-name}-minio`                               |  1 |
| `{release-name}-rabbitmq`                            |  1 |
| `{release-name}-ibm-postgressql-proxy`               |  2 |
| `{release-name}-ibm-postgressql-sentinel`            |  3 |
| `{release-name}-ibm-postgressql-keeper`              |  3 |

| Statefulset                  | Number of replicas |
|-------------------------|-------------------|
| `{release-name}-ibm-postgresql-keeper` | 3          |
| `{release-name}-ibm-rabbitmq `         | 3          |

The standard installation (*development configuration*) requires a total of **14.75** CPUs and **38.5** GB of memory. These numbers are based on a standard installation that includes the US English models only. In general, the memory requirements vary depending on which models you include in the installation.

### Setting the sessions/CPU ratio
{: #stt-set-sessions-cpu}

The meaning of a **session** in this context is one of the following:
  - `recognize` request to the STT runtime
  - `synthesize` request to the TTS runtime
  - `train` request to the STT Customization backend (STT AM Patcher)

To choose resources for each of the session types, perform the following calculations.

#### STT Runtime (`recognize`)
{: #stt-recognize}

STT runtime requires `R=0.6` CPU per `recognize` session. The calculation is done as follows:

1. Set the maximum number of sessions (`S`) you want to run in parallel; for example. `S=13`.
2. Calculate number of CPUs (`N`) needed to process `S` sessions as follows: `N = S * R = S * 0.6`
3. Round up `N` to the closest integer.

**Example**

Let's assume that you want to run up to `13` recognize session in parallel.

 ```
    N = S * R = 13 * 0.6 = 7.8 ~= 8 [CPUs]
 ```

 You need to set the value `sttRuntime.groups.sttRuntimeDefault.resources.requestsCpu=8` during installation.


#### TTS Runtime (`synthesize`)
{: #tts-synthesize}

TTS runtime requires `R=0.4` CPU per `synthesis` session. The calculation is done as follows:

1. Set the maximum number of sessions (`S`) you want to run in parallel; for example, `S=13`.
2. Calculate number of CPUs (`N`) needed to process `S` sessions as follows: `N = S * R`.
3. Round up `N` to the closest integer.

**Example**

Let's assume that you want to run up to `13` synthesize sessions in parallel.

```
    N = S * R = 13 * 0.4 = 5.2 ~= 6 [CPUs]
```

 You need to set the value `ttsRuntime.groups.ttsRuntimeDefault.resources.requestsCpu=6` during installation.

With the TTS Runtime, it is also possible to change `R` by setting `global.ttsVoiceMarginalCPU` to achieve a better *session:CPU* ratio without endangering *Real Time Factor*.


#### STT Customization backend (`train`)
{: #stt-customization-backend}

The STT Customization backend requires at least `1` CPU per training session. However, a training session can be parallelized on its own because the most of the calculations in the backend can run on multiple CPUs. One training session can use multiple threads (`T`) for processing, which means that one training session requires `T` CPUs per session. It is basically the same as setting `R=T` for STT runtime. Choosing `T>1` means faster training to some extent.

The following table shows the relation between the number of threads and processing time (done with 112 minutes of audio data):

Threads | Traning duration (minutes) | Speed-up (compared to 1 thread) |
--------|----------------------------|---------------------------------|
1       | 118.6                      | 1.00                            |
2       | 65.8                       | 1.80                            |
3       | 49.2                       | 2.41                            |
4       | 40.6                       | 2.92                            |
5       | 37.6                       | 3.15                            |
6       | 37.2                       | 3.19                            |

As you can see, *speed up* starts slowing down with `T=4`, so using more than 4 threads per session does not improve performance.

Overall calculation of CPU requirements for the STT Customization backend is done as follows. All input values must be whole numbers; for example, 1, 2, 3, 4, and so on.

1. Set the number of parallel train session (`S`) you want to run; for example, `S=2`.
1. Set the number of parallel threads per session (`T`) you want to utilize; for example, `T=2`.
1. Calculate the number of CPUs (`N`) needed to process `S` session as follows: `N = S * T`.

**Example**

 Let's assume that you want to run `2` training session in parallel with utilizing `3` threads per session to achieve reasonable performance.

 ```
    N = S * T = 2 * 3 = 6 [CPUs]
 ```

 You need to set the following values:
 ```
  sttAMPatcher.groups.sttAMPatcher.resources.requestsCpu=6
  sttAMPatcher.groups.sttAMPatcher.resources.threads=3
 ```

### Dynamic resource calculation
{: #stt-dynamic-resource-calculation}

The STT Runtime, TTS Runtime, and STT Customization backend components support automatic required memory resource calculation, which is based on the selected number of CPUs and the selected language models. Automatic resource calculation is enabled by default. You can modify this behavior by setting the following values to `true` or `false` as needed:

```
sttRuntime.groups.sttRuntimeDefault.resources.dynamicMemory
ttsRuntime.groups.ttsRuntimeDefault.resources.dynamicMemory
sttAMPatcher.groups.sttAMPatcher.resources.dynamicMemory
```

When you set any of the previous values to `false`, you must specify the required memory yourself, as described in [Options](#options).

  Disabling automatic resource calculation is not recommended and can cause undesired service behavior.
  {: important}

## Installing the chart
{: #stt-install-options}

You can install the chart on either of the following platforms:
  - [Installing the chart on IBM Cloud Pak for Data (without Red Hat OpenShift)](#install-without-openshift)
  - [Installing the chart on IBM Cloud Pak for Data with Red Hat OpenShift](#install-with-openshift)

## Installing the chart on IBM Cloud Pak for Data (without Red Hat OpenShift)
{: #install-without-openshift}

Follow these instructions to deploy a single IBM Watson Speech Services instance on a stand-alone IBM Cloud Pak for Data cluster.

### Software prerequisites
{: #no-openshift-sw-prereqs}

- IBM Cloud Pak for Data v2.1.0.1 or v2.5
- Kubernetes v1.12.4 or later
- Helm v2.9.1 or later

### PodSecurityPolicy requirements
{: #no-openshift-psp-reqs}

The predefined PodSecurityPolicy name [`ibm-restricted-psp`](https://ibm.biz/cpkspec-psp) has been verified for this chart. If your target namespace is bound to this PodSecurityPolicy, you can skip the rest of this section and proceed to install the chart.

Additionally, this chart also defines a custom PodSecurityPolicy that can be used to finely control the permissions and capabilities needed to deploy this chart. You can enable this custom PodSecurityPolicy by using the user interface or the supplied instructions and scripts in the `pak_extension` pre-install directory.

- From the user interface, you can copy and paste the following snippets to enable the custom PodSecurityPolicy.
  - Custom PodSecurityPolicy definition:

    ```yaml
    apiVersion: extensions/v1beta1
    kind: PodSecurityPolicy
    metadata:
      name: ibm-speech-psp
    spec:
      allowPrivilegeEscalation: false
      forbiddenSysctls:
      - '*'
      fsGroup:
        ranges:
        - max: 65535
          min: 1
        rule: MustRunAs
      requiredDropCapabilities:
      - ALL
      runAsUser:
        rule: MustRunAsNonRoot
      seLinux:
        rule: RunAsAny
      supplementalGroups:
        ranges:
        - max: 65535
          min: 1
        rule: MustRunAs
      volumes:
      - configMap
      - emptyDir
      - projected
      - secret
      - downwardAPI
      - persistentVolumeClaim
    ```

  - Custom ClusterRole for the custom PodSecurityPolicy:

    ```yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRole
    metadata:
      name: ibm-speech-psp
    rules:
    - apiGroups:
      - extensions
      resourceNames:
      - ibm-chart-dev-psp
      resources:
      - podsecuritypolicies
      verbs:
      - use
    ```

### Installing the chart
{: #no-openshift-install}

  The `cluster-admin` role is required to deploy IBM Watson Speech Services.
  {: important}

1.  From the Kubernetes command line tool, create the namespace in which to deploy the service; for example, `speech-services`. Use the following command to create the namespace:

    ```sh
    kubectl create namespace {namespace-name}
    ```

    If you cannot access the Kubernetes command line tool, see [Enabling access to kubectl CLI](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html) for instructions.

1.  To load the file from Passport Advantage into IBM Cloud Private, enter the following command in the IBM Cloud Private command line interface.

    ```sh
    cloudctl catalog load-archive --registry https://{cluster4d-master-node}:8500/{namespace-name} --archive {compressed-file-name} --repo local-charts
    ```

    - `{compressed-file-name}` is the name of the PPA file that you downloaded from Passport Advantage.
    - `{cluster4d-master-node}` is the URL of the master node within the IBM Cloud Pak for Data cluster.
    - `{namespace-name}` is the Kubernetes and Docker namespace created in the previous step.

1.  If you have a pre-existing version of the service on your cluster, remove the associated `ibm-watson-speech-prod-{release_number}.tgz` file.

1.  Run the following command to download the chart from the IBM Cloud Private repository:

    ```sh
    wget https://{cluster_CA_domain}:8443/helm-repo/requiredAssets/ibm-watson-speech-prod-1.1.2.tgz --no-check-certificate
    ```

1.  Extract the TAR file from the TGZ file, and then extract files from the TAR file by using the following command:

    ```sh
    tar -xvf /path/to/ibm-watson-speech-prod-1.1.2.tgz
    ```

1.  Create persistent volumes for the service.

    - For a production deployment, consider using an IBM Cloud Pak for Data storage add-on or a storage option that is hosted outside the cluster.
    - For a development deployment, you can use the `createLocalPVs.sh` script that is provided in the archive to create the local storage volumes.
    - If you want to use [Portworx](https://portworx.com/) as the persistent storage solution, see [Using Portworx as a storage solution](#use-portworx).

1.  Set up required labels.

    A label must be added to the namespace where IBM Cloud Pak for Data is installed (normally `zen`). The label is needed to permit communication between your application's namespace and the IBM Cloud Pak for Data namespace by using a network policy. To meet this requirement there are cluster-scoped pre and post actions that need to occur. Run the script that is provided with the archive to add the label.

    ```sh
    cd {compressed-file-dir}/charts/ibm-watson-speech-prod/ibm_cloud_pak/pak_extensions/pre-install/clusterAdministration
    ./labelNamespace.sh {namespace-name}
    ```

    where `{namespace-name}` is the namespace where IBM Cloud Pak for Data is installed (normally `zen`).

1.  Create the image policy.

    For each image in a repository, an image policy scope of either cluster or namespace is applied. When you deploy an application, IBM Container Image Security Enforcement checks whether the Kubernetes namespace that you are deploying to has any policy regulations that must be applied.

    1. Create an `image_policy.yaml` file with the following content:

      ```yaml
      apiVersion: securityenforcement.admission.cloud.ibm.com/v1beta1
      kind: ClusterImagePolicy
      metadata:
       name: watson-speech-services-{name}-policy
      spec:
       repositories:
          - name: "{cluster4d-master-node}:8500/*"
            policy:
              va:
                enabled: false
      ```

       Replace the following variables with the appropriate values for your cluster:

        - `{cluster4d-master-node}`: The hostname of the master node within the IBM Cloud Pak for Data cluster.
        - `{name}`: A name that helps you identify this deployment. You can use the version number of the product, such as `1.1.2`.

    1. Apply the policy by running the following command:

      ```sh
      kubectl apply -f ./image_policy.yaml
      ```

1.  Create secrets

    Two secret objects need to be created manually within the `{namespace-name}` namespace to set the access credentials for the Minio and PostgreSQL datastores. To set credentials for Minio see [Secrets](#minio-secrets) under [Configuring Minio object storage](#config-minio). To set credentials for PostgreSQL and RabbitMQ, see [Configuring the PostgreSQL and RabbitMQ installations](#stt-config-postgresql-rabbitmq).

    Quickstart: Create the following two secrets for Minio and PostgreSQL.
    - Minio
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: minio
      type: Opaque
      data:
        accesskey: YWRtaW4=
        secretkey: YWRtaW4xMjM0
      ```

      where `accesskey` and `secretkey` are values of your choice encoded in `base64`; for example:
      ```sh
      echo -n "admin" | base64
      YWRtaW4=

      echo -n "admin1234" | base64
      YWRtaW4xMjM0
      ```
    - PostgreSQL
      ```yaml
      apiVersion: v1
      data:
        pg_repl_password: cmVwbHVzZXI=
        pg_su_password: c3RvbG9u
      kind: Secret
      metadata:
        name: user-provided-postgressql # this name can be anything you choose
      type: Opaque
      ```
      where both `pg_repl_password` and `pg_su_password` are values of your choice encoded in `base64`.

1.  Edit values in the `values.yaml` file, which is stored in the `{compressed-file-dir}/charts/ibm-watson-speech-prod` directory.

    At minimum, you must provide your own values for the following configurable settings:

      - Set `global.icpDockerRepo` to the Docker registry URL, including the namespace; for example, `docker-registry.default.svc:5000/{namespace-name}`.
      - Set `global.imagePullSecretName` to the name of the Docker registry secret, which is `sa-{namespace-name}`. You can verify that the secret actually exists in your namespace by running `kubectl get secrets -n {namespace-name}`.
      - Set `global.image.repository` to the same value you set `global.icpDockerRepo`.
      - Set `global.image.pullSecret` to the same value you set `global.imagePullSecretName`.

  See [Select the components to install](#select-components) for information on how to select the components to install. Additionally, see [Configuration](#stt-configuration) to learn more about the installation configuration.

1.  After you define any custom configuration settings, you can install the chart from the Helm command line interface. Enter the following command from the directory where the package was loaded in your local system:

    ```sh
    helm install --namespace {namespace-name} --name {release-name} ./ibm-watson-speech-prod
    ```

    - `{namespace-name}` is the name of the namespace where the Helm chart is to be installed.
    - `{release-name}` is the name of the Helm release that is to be installed.

1.  Verify the installation as described in [Verifying the chart](#stt-verify).

## Installing the chart on IBM Cloud Pak for Data with Red Hat OpenShift
{: #install-with-openshift}

Follow these instructions to deploy a single IBM Watson Speech Services instance on an IBM Cloud Pak for Data cluster running on Red Hat OpenShift.

### OpenShift software prerequisites

- IBM Cloud Pak for Data v2.1.0.1 or v2.5
- Kubernetes v1.12.4 or later
- Helm v2.9.1 or later

Before installing the Speech Services solution, you must install and configure [`helm`](https://helm.sh/docs/using_helm/#installing-the-helm-client) and [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html).

### Red Hat OpenShift SecurityContextConstraints Requirements

This chart requires a SecurityContextConstraints to be bound to the target namespace prior to installation. To meet this requirement there might be cluster-scoped as well as namespace-scoped before and after actions that need to be performed.

The predefined SecurityContextConstraints name [`restricted`](https://ibm.biz/cpkspec-scc) has been verified for this chart. If your target namespace is bound to this SecurityContextConstraints resource you can skip the rest of this section and proceed to install the chart. Otherwise, run the following command to bind the `restricted` SecurityContextConstraints to your namespace:

```sh
oc adm policy add-scc-to-group restricted system:serviceaccounts:{namespace-name}
```

This chart also defines a custom SecurityContextConstraints that can be used to finely control the permissions and capabilities needed to deploy this chart. You can enable this custom SecurityContextConstraints resource using the supplied instructions and scripts in the `pak_extension` pre-install directory.

- From the user interface, you can copy and paste the following snippets to enable the custom SecurityContextConstraints:
  - Custom SecurityContextConstraints definition:
    ```
    fsGroup:
      type: MustRunAs
    groups:
    - system:authenticated
    kind: SecurityContextConstraints
    metadata:
      name: ibm-speech-scc
    priority: null
    readOnlyRootFilesystem: false
    requiredDropCapabilities:
    - KILL
    - MKNOD
    - SETUID
    - SETGID
    runAsUser:
      type: MustRunAsRange
    seLinuxContext:
      type: MustRunAs
    supplementalGroups:
      type: RunAsAny
    users: []
    volumes:
    - configMap
    - downwardAPI
    - emptyDir
    - persistentVolumeClaim
    - projected
    - secret
    ```    

- From the command line, you can run the setup scripts included under `pak_extensions`.

  For cluster admin, the pre-install instructions are located at:
  - `pre-install/clusterAdministration/Notes.md`

  For team admin, the namespace-scoped instructions are located at:
  - `pre-install/namespaceAdministration/Notes.md`

### Installing the chart

  The `cluster-admin` role is required to deploy IBM Watson Speech Services.
  {: important}

1.  Log into OpenShift and Docker:

    ```sh
    oc login
    docker login -u $(oc whoami) -p $(oc whoami -t) {docker-registry}
    ```

    - `{docker-registry}` is the address of the OpenShift Docker registry; for example,  `docker-registry-default.apps.speech-openshift.ibm.com`. You can find the URL of the Docker registry in the OpenShift console. You might need to add `{docker-registry}` to your list of insecure registries in your local Docker preferences.

1.  From the OpenShift command line tool, create the namespace in which to deploy the service; for example, `speech-services`. Use the following command to create the namespace:

    ```bash
    oc new-project {namespace-name}
    ```

1.  Make sure you are pointing at the correct OpenShift project:

    ```bash
    oc project {namespace-name}
    ```

    - `{namespace-name}` is the Kubernetes and Docker namespace that you created in the previous step.

1.  Extract the PPA archive contents:

    ```sh
    cd {compressed-file-dir}
    tar -xvf {compressed-file-name}
    cd charts
    tar -xvf ibm-watson-speech-prod-1.1.2.tgz
    ```

    - `{compressed-file-dir}` is the directory to which you downloaded {compressed-file-name}.
    - `{compressed-file-name}` is the name of the PPA file that you downloaded from Passport Advantage.

1.  Load the Docker images into the OpenShift Docker registry:

    ```sh
    cd {compressed-file-dir}/charts/ibm-watson-speech-prod/ibm_cloud_pak/pak_extensions/pre-install/clusterAdministration
    ./loadImagesOpenShift.sh --path {compressed-file-dir} --namespace {namespace-name} --registry {docker-registry}
    ```

    - `{docker-registry}` is the address of the OpenShift Docker registry.

    If successful, the Docker images now exist in the OpenShift Docker registry.

    If you cannot access the Kubernetes command line tool, see [Enabling access to kubectl CLI](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html) for instructions.

1.  Create persistent volumes for the service.

    - For a production deployment, consider using an IBM Cloud Pak for Data storage add-on or a storage option that is hosted outside the cluster.
    - For a development deployment, you can run `createLocalPVs.sh` from inside the cluster to create the local storage volumes. The script is located at `ibm_cloud_pak/pak_extensions/pre-install/clusterAdministration`.
    - If you want to use [Portworx](https://portworx.com/) as the persistent storage solution, see [Using Portworx as a storage solution](#use-portworx).

1.  Set up required labels.

    A label must be added to the namespace where IBM Cloud Pak for Data is installed (usually `zen`). To meet this requirement there are cluster-scoped before and after actions that need to occur. Run the script that is provided with the archive to add the label.

    ```sh
    cd {compressed-file-dir}/charts/ibm-watson-speech-prod/ibm_cloud_pak/pak_extensions/pre-install/clusterAdministration
    ./labelNamespace.sh {namespace-name}
    ```

    where `{namespace-name}` is the namespace where IBM Cloud Pak for Data is installed (normally `zen`).

1. Create secrets.

    Two secret objects need to be created manually within the `{namespace-name}` namespace to set the access credentials for the Minio and PostgreSQL datastores. To set credentials for Minio see [Secrets](#minio-secrets) under [Configuring Minio object storage](#config-minio). To set credentials for PostgreSQL and RabbitMQ, see [Configuring the PostgreSQL and RabbitMQ installations](#stt-config-postgresql-rabbitmq).

    Quickstart: Create the following two secrets for Minio and PostgreSQL.
    - Minio
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: minio
      type: Opaque
      data:
        accesskey: YWRtaW4=
        secretkey: YWRtaW4xMjM0
      ```

      where `accesskey` and `secretkey` are values of your choice encoded in `base64`; for example:

      ```sh
      echo -n "admin" | base64
      YWRtaW4=

      echo -n "admin1234" | base64
      YWRtaW4xMjM0
      ```
    - PostgreSQL
      ```yaml
      apiVersion: v1
      data:
        pg_repl_password: cmVwbHVzZXI=
        pg_su_password: c3RvbG9u
      kind: Secret
      metadata:
        name: user-provided-postgressql # this name can be anything you choose
      type: Opaque
      ```
      where again both `pg_repl_password` and `pg_su_password` are your choice and base64 encoded.

1.  Fetch the Docker registry secret that is to be used to pull images within the cluster (`imagePullSecret`):

    ```sh
    oc get secrets | grep default-dockercfg
    ```

1.  Edit values in the `values.yaml` file, which is stored in the `{compressed-file-dir}/charts/ibm-watson-speech-prod` directory.

    At a minimum, you must provide your own values for the following configurable settings:

      - Set `global.icpDockerRepo` to the Docker registry URL, including the namespace. For example, `docker-registry.default.svc:5000/{namespace-name}`.
      - Set `global.imagePullSecretName` to the name of the Docker registry secret obtained in the previous step.
      - Set `global.image.repository` to the same value you set `global.icpDockerRepo`.
      - Set `global.image.pullSecret` to the same value you set `global.imagePullSecretName`.

    See the section *Select the components to install* for information on how to select the components to install. Additionally, read the *Installation appendix* and *Configuration* section to learn more about the installation configuration.

1.  After you define any custom configuration settings, you can install the chart from the Helm command line interface. Enter the following command from the directory where the package was loaded in your local system:

    ```sh
    helm install --namespace {namespace-name} --name {release-name} {compressed-file-dir}/charts/ibm-watson-speech-prod/ --tiller-namespace {tiller-namespace}
    ```

    - `{tiller-namespace}` is the namespace where Tiller is installed within the cluster (typically the `zen` namespace).
    - `{release-name}` is the name of the Helm release.

1.  Verify the installation as described in [Verifying the chart](#stt-verify).

## Verifying the Chart
{: #stt-verify}

See the instructions from the `NOTES.txt` within the chart after the Helm installation completes for chart verification. The instructions can also be viewed by running the command `helm status my-release --tls`.

## Configuration
{: #stt-configuration}

The Helm chart has the following values that you can override by using the `--set` parameter with the `install` command.

### Language model selection
{: #lang-model-selection}

You can perform an installation that includes only a subset of the language models/voices in the catalog. Installing all of the models/voices in the catalog substantially increases the memory requirements. Therefore, it is strongly recommended that you install only those languages that you intend to use.

You can select the languages to be installed by checking or unchecking each of the models/voices in the `global.sttModels.*` or `global.ttsVoices.*` values. By default, the dynamic resource calculation feature is enabled; it automatically computes the exact amount of memory that is required for the selected models/voices.

It is also possible to install ad hoc models/voices that was not released with this version. You need to download a special package containing data for the models/voices, upload it into the cluster the same way as main package, and specify the following options during installation.

| Value                                           | Description                                             |
|-------------------------------------------------|---------------------------------------------------------|
| `global.sttModels.$modelName.catalogName`       | Model name as it is found in catalog.                   |
| `global.sttModels.$modelName.size`              | Memory footprint used to calculate memory requirements. |
| `global.ttsVoices.$voiceName.catalogName`       | Voice name as it is found in catalog.                   |
| `global.ttsVoices.$voiceName.size`              | Memory footprint used to calculate memory requirements. |

**Example:**

Let's assume that there is a new broadband model for the Czech language that was released as an ad-hoc model for the current Speech release. To enable it during update, specify the following options during installation:

In this example, `$modelName` is `csCSBroadbandModel` and `$catalogName` is `cs-CS_BroadBandModel`.

```sh
   helm upgrade RELEASE CHART --set global.sttModels.csCSBroadbandModel.catalogName=cs-CS_BroadBandModel --set global.sttModels.csCSBroadbandModel.size=500 [OTHER-FLAGS]
```

### Storage of customer data (STT Runtime and AMC Patcher)
{: #storage-of-customer-data}

By default, payload data, including audio files, recognition hypotheses, and annotations, are temporarily stored in the running container. You can disable this behavior by checking the `STT Runtime | Disable storage of customer data` option. Checking this option also removes sensitive information from container logs.

### Options
{: #options}

The following options apply to an IBM Watson Speech Services runtime configuration.

#### Components
{: #list-of-components}

There are five components that can be enabled or disabled according to your needs. The main components are **Speech-to-Text runtime** and **Text-to-Speech runtime**. Additional components are **Speech-to-Text Customization**, **Text-to-Speech Customization**, and **Speech-to-Text Async**.

| Value                           | Description                                                                                                                                                                       | Default |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| `tags.sttRuntime`               | Speech-to-Text Runtime that is the base component for recognition. If you check any of the Speech-to-Text additional components, the Speech-to-Text runtime is enabled automatically. | `true`  |
| `tags.ttsRuntime`               | Text-to-Speech Runtime that is the base component for recognition. If you check any of the Text-to-Speech additional components, the Text-to-Speech runtime is enabled automatically. | `true`  |
| `tags.sttCustomization`         | Speech-to-Text Customization component. Enabling it also enables the Speech-to-Text runtime if `tags.sttRuntime=false`.                                                               | `true`  |
| `tags.ttsCustomization`         | Text-to-Speech Customization component. Enabling it also enables the Text-to-Speech runtime if `tags.sttRuntime=false`.                                                               | `true`  |
| `tags.sttAsync`                 | Speech-to-Text Async component.                                                                                                                                                   | `true`  |

#### Datastores
{: #list-of-datastores}

| Value                                               | Description                                                                                                                     | Default                      |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| `external.minio.mode`                               | Sets Minio server mode (`standalone`, `distributed`).                                                                           | `distributed`                |
| `external.minio.persistence.size`                   | Size of persistent volume claim (PVC).                                                                                          | `100Gi`                      |
| `external.minio.replicas`                           | Number of nodes (applicable only for Minio distributed mode). Must be 4 <= x <= 32.                                             | `4`                          |
| `external.minio.minioAccessSecret`                  | Create a secret that contains base64-encoded accesskey (5 - 20 characters) and secretkey (8 - 40 characters). The keys are used to access the Minio Object Server. You need to create the secret in the same namespace in which you deploy the chart. | `minio`                                                   |
| `global.datastores.minio.secretName`                | Minio object storage access secret name created as an installation prerequisite.                                                | `minio`                      |
| `global.datastores.postgressql.auth.authSecretName` | PostgresSQL name of the secrets object that contains the credentials to access the datastore.                                   | `user-provided-postgressql`  |
| `postgressql.auth.authSecretName`                   | PostgresSQL name of the secrets object that contains the credentials to access the datastore.                                   | `user-provided-postgressql`  |


#### Anonymize logs and audio data
{: list-of-anonymize-logs-and-audio-data}

| Value                               | Description                                      | Default  |
|-------------------------------------|--------------------------------------------------|----------|
| `sttRuntime.anonymizeLogs`          | Opt out of runtime logs and audio data.          | `False`  |
| `ttsRuntime.anonymizeLogs`          | Opt out of runtime logs and audio data.          | `False`  |
| `sttAMPatcher.anonymizeLogs`        | Opt out of runtime logs and audio data.          | `False`  |


#### Resources
{: #resources}

##### Speech-to-Text runtime
{: #stt-runtime-resources}

| Value                                                          | Description                                                                                                                              | Default   |
|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| `sttRuntime.groups.sttRuntimeDefault.resources.dynamicMemory`  | Calculate memory requirements for STT runtime according to selected models. For more information, see the chart Overview.                | `True`    |
| `sttRuntime.groups.sttRuntimeDefault.resources.requestsCpu`    | Requested CPUs for STT runtime. Minimal value is 4.                                                                                      | `8`       |
| `sttRuntime.groups.sttRuntimeDefault.resources.requestsMemory` | Calculation of the memory requirements can be found in the chart Overview. When dynamic memory is enabled, this option has no effect.    | `22000Mi` |

##### Text-to-Speech runtime
{: #tts-runtime-resources}

| Value                                                          | Description                                                                                                                              | Default   |
|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| `ttsRuntime.groups.ttsRuntimeDefault.resources.dynamicMemory`  | Calculate memory requirements for the TTS runtime according to the selected models. For more information, see the chart overview.                | `True`    |
| `ttsRuntime.groups.ttsRuntimeDefault.resources.requestsCpu`    | Requested CPUs for the TTS runtime. Minimal value is 4.                                                                                      | `8`       |
| `ttsRuntime.groups.ttsRuntimeDefault.resources.requestsMemory` | Calculation of the memory requirements can be found in the chart overview. When dynamic memory is enabled, this option has no effect.    | `22000Mi` |
| `global.ttsVoiceMarginalCPU`                                   | TTS Voice marginal CPU used for synthesis. The value is in milli-CPUs.                                                                    | `400`     |

##### Speech-to-Text customization backend (Acoustic Model Patcher)
{: #stt-customization-resources}

| Value                                                          | Description                                                                                                                              | Default   |
|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| `sttAMPatcher.groups.sttAMPatcher.resources.dynamicMemory`     | Calculate memory requirements for STT AMC patcher according to the selected models. For more information, see the chart Overview.            | `True`    |
| `sttAMPatcher.groups.sttAMPatcher.resources.requestsCpu`       | Each customization session needs 4 CPUs.                                                                                                | `8`       |
| `sttAMPatcher.groups.sttAMPatcher.resources.requestsMemory`    | The amount of memory depends on the number of CPUs. Size can be calculated as the number of CPUs * 3 GB.                                                      | `22000Mi` |
| `sttAMPatcher.groups.sttAMPatcher.resources.threads`           | Number of parallel-processing threads for AMC. Note that fewer threads means longer training time.                                       | `4`       |

#### Speech-to-Text models
{: #stt-models}

| Value                                                     | Description                                                                               | Default |
|-----------------------------------------------------------|-------------------------------------------------------------------------------------------|---------|
| `global.sttModels.enUsBroadbandModel.enabled`             | Whether to include the en-US Broadband Model in the installation.                         | `True`  |
| `global.sttModels.enUsNarrowbandModel.enabled`            | Whether to include the en-US Narrowband Model in the installation.                        | `True`  |
| `global.sttModels.enUsShortFormNarrowbandModel.enabled`   | Whether to include the en-US ShortForm Narrowband Model in the installation.         | `True`  |
| `global.sttModels.jaJpBroadbandModel.enabled`             | Whether to include the jp-JP Broadband Model in the installation.                         | `False` |
| `global.sttModels.jaJpNarrowbandModel.enabled`            | Whether to include the jp-JP Narrowband Model in the installation.                        | `False` |
| `global.sttModels.koKrBroadbandModel.enabled`             | Whether to include the ko-KR Broadband Model in the installation.                         | `False` |
| `global.sttModels.koKrNarrowbandModel.enabled`            | Whether to include the ko-KR Narrowband Model in the installation.                        | `False` |
| `global.sttModels.esEsBroadbandModel.enabled`             | Whether to include the es-ES Broadband Model in the installation.                         | `False` |
| `global.sttModels.esEsNarrowbandModel.enabled`            | Whether to include the es-ES Narrowband Model in the installation.                        | `False` |
| `global.sttModels.frFrBroadbandModel.enabled`             | Whether to include the fr-FR Broadband Model in the installation.                         | `False` |
| `global.sttModels.frFrNarrowbandModel.enabled`            | Whether to include the fr-FR Narrowband Model in the installation.                        | `False` |
| `global.sttModels.arArBroadbandModel.enabled`             | Whether to include the ar-AR Broadband Model in the installation                          | `False` |
| `global.sttModels.deDeBroadbandModel.enabled`             | Whether to include the de-DE Broadband Model in the installation                          | `False` |
| `global.sttModels.deDeNarrowbandModel.enabled`            | Whether to include the de-DE Narrowband Model in the installation                         | `False` |
| `global.sttModels.enGbBroadbandModel.enabled`             | Whether to include the en-GB Broadband Model in the installation                          | `False` |
| `global.sttModels.enGbNarrowbandModel.enabled`            | Whether to include the en-GB Narrowband Model in the installation                         | `False` |
| `global.sttModels.ptBrBroadbandModel.enabled`             | Whether to include the pt-BR Broadband Model in the installation                          | `False` |
| `global.sttModels.ptBrNarrowbandModel.enabled`            | Whether to include the pt-BR Narrowband Model in the installation                         | `False` |
| `global.sttModels.zhCnBroadbandModel.enabled`             | Whether to include the zh-CN Broadband Model in the installation                          | `False` |
| `global.sttModels.zhCnNarrowbandModel.enabled`            | Whether to include the zh-CN Narrowband Model in the installation                         | `False` |

#### Text-to-Speech voices
{: #tts-voices}

| Value                                           | Description                                                               | Default |
|-------------------------------------------------|---------------------------------------------------------------------------|---------|
| `global.ttsVoices.enUSMichaelV3Voice.enabled`   | Whether to include the en-US Michael LPC Net Voice in the installation    | `True`  |
| `global.ttsVoices.enUSAllisonV3Voice.enabled`   | Whether to include the en-US Allison LPC Net Voice in the installation    | `True`  |
| `global.ttsVoices.enUSLisaV3Voice.enabled`      | Whether to include the en-US Lisa LPC Net Voice in the installation       | `True`  |
| `global.ttsVoices.deDEBirgitV3Voice.enabled`    | Whether to include the de-DE Birgit LPC Net Voice in the installation     | `False` |
| `global.ttsVoices.deDEDieterV3Voice.enabled`    | Whether to include the de-DE Dieter LPC Net Voice in the installation     | `False` |
| `global.ttsVoices.enGBKateV3Voice.enabled`      | Whether to include the en-GB Kate LPC Net Voice in the installation       | `False` |
| `global.ttsVoices.esLASofiaV3Voice.enabled`     | Whether to include the es-LA Sofia LPC Net Voice in the installation      | `False` |
| `global.ttsVoices.esUSSofiaV3Voice.enabled`     | Whether to include the es-US Sofia LPC Net Voice in the installation      | `False` |
| `global.ttsVoices.ptBRIsabelaV3Voice.enabled`   | Whether to include the pt-BR Isabela LPC Net Voice in the installation    | `False` |
| `global.ttsVoices.esESEnriqueV3Voice.enabled`   | Whether to include the es-ES Enrique LPC Net Voice in the installation    | `False` |
| `global.ttsVoices.esESLauraV3Voice.enabled`     | Whether to include the es-ES Laura LPC Net Voice in the installation      | `False` |
| `global.ttsVoices.frFRReneeV3Voice.enabled`     | Whether to include the fr-FR Renee LPC Net Voice in the installation      | `False` |
| `global.ttsVoices.itITFrancescaV3Voice.enabled` | Whether to include the it-IT Francesca LPC Net Voice in the installation  | `False` |
| `global.ttsVoices.jaJPEmiVoice.enabled`         | Whether to include the ja-JP Emi Voice in the installation                | `False` |
