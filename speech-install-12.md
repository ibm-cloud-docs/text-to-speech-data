---

copyright:
  years: 2020
lastupdated: "2020-12-09"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:gif: data-image-type='gif'}

# Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} version 1.2
{: #speech-install-12}

This and the following pages provide information about installing and managing {{site.data.keyword.speechtotextdatafull}} and {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}. The two services share a common installation and common datastores to allow for more efficient resource consumption and simplified support. Most of the installation information therefore applies to both services.
{: shortdesc}

The following pages often refer to the combination of {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} as *Speech services.* Information specific to just one of the two services is clearly identified.

These instructions apply to version 1.2 of the Speech services. For information about installing and managing version 1.1.4 of the services, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} version 1.1.4](/docs/text-to-speech-data?topic=text-to-speech-data-speech-install).
{: note}

## Where to begin
{: #speech-install-begin-12}

See the following topics in the IBM Knowledge Center for the information that you need to get started with the {{site.data.keyword.watson}} Speech services.

-   *To install a new deployment of the service:*

    -   [Setting up the cluster for {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-text/tts-svc-install-adm.html){: external}
    -   [Creating an override file for {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} installation](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-text/tts-svc-override.html){: external}
    -   [Installing the {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} service](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-text/tts-svc-install.html){: external}

<!--
-   *To upgrade an existing deployment of the service:*

    -   [Preparing to upgrade {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-text/tts-svc-upgrade-adm.html){: external}
    -   [Upgrading {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-text/tts-upgrade-svc.html){: external}
-->

-   *To uninstall the service:*

    -   [Uninstalling {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_latest/svc-text/tts-svc-uninstall.html){: external}

## Where to continue
{: #speech-install-continue-12}

See the following pages for more information about installation and configuration parameters, and post-deployment management activities.

| Page | Contents |
|------|----------|
| [Using the override file](/docs/text-to-speech-data?topic=text-to-speech-data-speech-override-12) | Using values in the `speech-override.yaml` file to specify aspects of the installation and configuration that are common to both Speech services, including datastores, or are specific to {{site.data.keyword.speechtotextshort}} or {{site.data.keyword.texttospeechshort}}. |
| [Managing your datastores](/docs/text-to-speech-data?topic=text-to-speech-data-speech-datastores-12) | Administering the MinIO and PostgreSQL datastores. For MinIO, topics include security secrets, operation mode, and storage. For PostgreSQL, the page describes security secrets. |
| [Managing your cluster](/docs/text-to-speech-data?topic=text-to-speech-data-speech-cluster-12) | A collection of basic cluster and service management procedures and information. Topics include managing user access, using common cluster management commands, setting Red Hat OpenShift SecurityContextConstraints, disabling storage of user data, and installing ad hoc models and voices. |
| [Scaling up your installation](/docs/text-to-speech-data?topic=text-to-speech-data-speech-scaling-12) | Scaling from a development configuration to a production configuration. Topics include scaling up PostgreSQL, RabbitMQ, and MinIO. Topics also include scaling up other aspects of the installation and setting the session-to-CPU ratio for the {{site.data.keyword.speechtotextshort}} runtime and customization AM patcher, and for the {{site.data.keyword.texttospeechshort}} runtime. |
| [Backing up and restoring your data](/docs/text-to-speech-data?topic=text-to-speech-data-speech-backup-12) | Backup and restore procedures for both disaster recovery and upgrade of your data. The procedures cover the MinIO and PostgreSQL datastores. |
{: caption="Table 1. Documentation overview and links"}
