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

# Scaling up your installation
{: #speech-scaling}

When you install the {{site.data.keyword.watson}} Speech services, you choose one of two configurations. The resources required for the installation, in terms of CPUs and memory, depend on the configuration you select.

-   The *development configuration* is used by the default installation. This configuration has a minimal footprint and is meant for development purposes and as a proof of concept. It can only handle several concurrent recognition sessions, and it is not highly available because some of the core components have no redundancy (they are single-replica).
-   The *production configuration* is a highly available solution that is intended to run production workloads. This configuration, which requires a minimum of three worker nodes, provides a highly available solution.

You can scale up from the development configuration to the production configuration after installing the solution by increasing the number of pods and replicas that are available for the deployment objects. How much to scale up each of the components depends on the degree of concurrency that you need. It is limited by the amount of hardware resources that are available in your Kubernetes cluster and namespace.

## Scaling up the PostgreSQL and RabbitMQ datastores
{: #speech-scaling-postgre}

By default, both PostgreSQL and RabbitMQ are installed with three replicas for high availability. Each replica is typically scheduled within a different Kubernetes worker node if resources allow. Before performing the installation, you can configure the number of replicas and the CPU and memory resources for each replica.

You can scale up the datastores on an already running solution by changing the number of replicas in the Deployment or StatefulSet objects. For example, you can scale up RabbitMQ as follows:

1.  Edit the StatefulSet object by running the following command:

    ```bash
    kubectl edit statefulsets {release}-ibm-rabbitmq
    ```
    {: pre}

1.  Change the value of the `spec.replicas:` attribute to the desired number of replicas.
1.  Save and close the StatefulSet object.

PostgreSQL has two Deployment objects:

-   `{release}-ibm-postgresql-proxy`
-   `{release}-ibm-postgresql-sentinel`

It also has a StatefulSet:

-   `ibm-wc-ibm-postgresql-keeper`

You can scale up the Deployment objects by running the following command:

```bash
kubectl scale --replicas={n} {deployment_object}
```
{: pre}

where `{n}` is the desired number of replicas for the specified Deployment (`{deployment_object}`). For example, the following command configures 3 replicas for PostgreSQL:

```bash
kubectl scale --replicas=3 deployment ibm-wc-ibm-postgresql-proxy
```
{: pre}

You can scale up the StatefulSet object by using the same commands. For StatefulSets, you need to create a sufficient number of persistent local volumes before scaling up the number of replicas so that the newly created pods can mount their volumes.

## Scaling up the rest of the solution
{: #speech-scaling-solution}

You can learn about the list of deployments (Kubernetes Deployment objects) by running the following command:

```bash
kubectl get deployment
```
{: pre}

You can then scale up the number of pods on each of the Deployment objects to match the number of pods in the production configuration by using the following command:

```bash
kubectl scale --replicas={n} deployment {deployment_object}
```
{: pre}

where `{n}` is the desired number of replicas for the given Deployment (`{deployment_object}`).

Table 1 shows the default number of replicas for Deployment objects.

<table>
  <caption>Table 1. Default number of replicas for Deployment objects</caption>
  <tr>
    <th>
      Deployment object
    </th>
    <th style="text-align:center">
      Default number of replicas
    </th>
  </tr>
  <tr>
    <td>
      `{release_name}-speech-to-text-stt-runtime`
    </td>
    <td style="text-align:center">
      1
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-speech-to-text-stt-customization`
    </td>
    <td style="text-align:center">
      1
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-speech-to-text-stt-am-patcher`
    </td>
    <td style="text-align:center">
      1
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-speech-to-text-stt-async`
    </td>
    <td style="text-align:center">
      1
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-speech-to-text-gdpr-data-deletion`
    </td>
    <td style="text-align:center">
      1
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-minio`
    </td>
    <td style="text-align:center">
      1
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-rabbitmq`
    </td>
    <td style="text-align:center">
      1
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-ibm-postgressql-proxy`
    </td>
    <td style="text-align:center">
      2
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-ibm-postgressql-sentinel`
    </td>
    <td style="text-align:center">
      3
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-ibm-postgressql-keeper`
    </td>
    <td style="text-align:center">
      3
    </td>
  </tr>
</table>

Table 2 shows the default number of replicas for StatefulSet objects.

<table>
  <caption>Table 2. Default number of replicas for StatefulSet objects</caption>
  <tr>
    <th>
      StatefulSet object
    </th>
    <th style="text-align:center">
      Default number of replicas
    </th>
  </tr>
  <tr>
    <td>
      `{release_name}-ibm-postgresql-keeper`
    </td>
    <td style="text-align:center">
      3
    </td>
  </tr>
  <tr>
    <td>
      `{release_name}-ibm-rabbitmq`
    </td>
    <td style="text-align:center">
      3
    </td>
  </tr>
</table>

The development configuration requires a total of 14.75 CPUs and 38.5 GB of memory. These numbers are based on a standard installation that includes the US English models and voices only. The memory requirements vary depending on which models and voices you include in the installation.

## Setting the session-to-CPU ratio
{: #speech-scaling-ratio}

As part of the scaling effort, you also need to consider the ratio of sessions to CPUs. The correct ratio can greatly improve the performance of your services. In this context, a *session* is one of the following:

-   A `recognize` request to the {{site.data.keyword.speechtotextshort}} runtime
-   A `synthesize` request to the {{site.data.keyword.texttospeechshort}} runtime
-   A `train` request to the {{site.data.keyword.speechtotextshort}} customization acoustic model (AM) patcher

The following sections describe how to calculate resources for each type of session.

### {{site.data.keyword.speechtotextshort}} runtime (recognize)
{: #speech-scaling-ratio-stt}

The {{site.data.keyword.speechtotextshort}} runtime requires 0.6 CPUs per recognize session. Let the following variables represent the parameters for the calculation:

-   `R` is the number of CPUs per recognize session, `R = 0.6`.
-   `S` is the maximum number of sessions that you want to run in parallel; for example, `S = 13`.
-   `N` is the number of CPUs that you need to process `S` sessions.

Calculate the number of CPUs that you need as follows, and round `N` up to the closest integer:

`N = S * R = S * 0.6`

For example, use the following equation to run 13 recognize sessions in parallel:

`N = S * R = 13 * 0.6 = 7.8 ~= 8 [CPUs]`

Set the value `sttRuntime.groups.sttRuntimeDefault.resources.requestsCpu=8`.

### {{site.data.keyword.texttospeechshort}} runtime (synthesize)
{: #speech-scaling-ratio-tts}

The {{site.data.keyword.texttospeechshort}} runtime requires 0.4 CPUs per synthesize session. Let the following values represents the parameters for the calculation:

-   `R` is the number of CPUs per synthesize session, `R = 0.4`.
-   `S` is the maximum number of sessions that you want to run in parallel; for example, `S = 13`.
-   `N` is the number of CPUs that you need to process `S` sessions.

Calculate the number of CPUs that you need as follows, and round `N` up to the closest integer:

`N = S * R = S * 0.4`

For example, use the following equation to run 13 synthesize sessions in parallel:

`N = S * R = 13 * 0.4 = 5.2 ~= 6 [CPUs]`

Set the value `ttsRuntime.groups.ttsRuntimeDefault.resources.requestsCpu=6`.

With the {{site.data.keyword.texttospeechshort}} Runtime, it is also possible to change `R` by setting `global.ttsVoiceMarginalCPU` to achieve a better *session:CPU* ratio without endangering the *Real Time Factor*.
{: note}

### {{site.data.keyword.speechtotextshort}} customization AM patcher (train)
{: #speech-scaling-ratio-stt-custom}

The {{site.data.keyword.speechtotextshort}} customization AM patcher requires at least 1.0 CPU per training session. However, a training session can be parallelized on its own because most of the calculations in the back-end (training) session can run on multiple CPUs.

One training session can use multiple threads (`T`) for processing, so one training session requires `T` CPUs per session. It is basically the same as setting `R = T` for the {{site.data.keyword.speechtotextshort}} runtime. Choosing `T > 1` generally means faster training.

Table 3 shows the relationship between the number of threads and the processing time for 112 minutes of audio data. As you can see, *speed up* begins to slow down with `T = 4` threads, so using more than 4 threads per session does not appreciably improve performance.

<table>
  <caption>Table 3. Relationship of threads to performance</caption>
  <tr>
    <th style="text-align:center">
      Threads
    </th>
    <th style="text-align:center">
      Training duration (in minutes)
    </th>
    <th style="text-align:center">
      Speed up (compared to 1 thread)
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      1
    </td>
    <td style="text-align:center">
     118.6
    </td>
    <td style="text-align:center">
      1.00
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      2
    </td>
    <td style="text-align:center">
      65.8
    </td>
    <td style="text-align:center">
      1.80
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      3
    </td>
    <td style="text-align:center">
      49.2
    </td>
    <td style="text-align:center">
      2.41
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      4
    </td>
    <td style="text-align:center">
      40.6
    </td>
    <td style="text-align:center">
      2.92
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      5
    </td>
    <td style="text-align:center">
      37.6
    </td>
    <td style="text-align:center">
      3.15
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      6
    </td>
    <td style="text-align:center">
      37.2
    </td>
    <td style="text-align:center">
      3.19
    </td>
  </tr>
</table>

The overall calculation of CPU requirements for the {{site.data.keyword.speechtotextshort}} customization AM patcher is done as follows. All input values must be whole numbers (for example, 1, 2, 3, and so on).

-   `S` is the number of parallel training sessions that you want to run; for example, `S = 2`.
-   `T` is the number of parallel threads per session that you want to use; for example, `T = 2`.
-   `N` is the number of CPUs needed to process `S` sessions in parallel.

Calculate the number of CPUs that you need to process `S` sessions in parallel as follows:

`N = S * T`

For example, use the following equation to run 2 training sessions in parallel and to use 3 threads per session to achieve reasonable performance:

`N = S * T = 2 * 3 = 6 [CPUs]`

Set the following values:

-   `sttAMPatcher.groups.sttAMPatcher.resources.requestsCpu=6`
-   `sttAMPatcher.groups.sttAMPatcher.resources.threads=3`
