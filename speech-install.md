---

copyright:
  years: 2019, 2021
lastupdated: "2021-04-09"

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

# Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} version 1.1.4
{: #speech-install}

This and the following pages provide information about installing and managing {{site.data.keyword.speechtotextdatafull}} and {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}. The two services share a common installation and common datastores to allow for more efficient resource consumption and simplified support. Most of the installation information therefore applies to both services.
{: shortdesc}

The following pages often refer to the combination of {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} as *Speech services.* Information specific to just one of the two services is clearly identified.
{: note}

## Where to begin
{: #speech-install-begin}

{{site.data.keyword.icp4dfull_notm}} 3.0.1 is deprecating support for Red Hat OpenShift 4.3 on 1 September 2020. Red Hat OpenShift 4.3 is going out of service on 22 October 2020. {{site.data.keyword.icp4dfull_notm}} is introducing support for Red Hat OpenShift 4.5. {{site.data.keyword.icp4dfull_notm}} is recommending that clients upgrade to Red Hat OpenShift 4.5 before 22 October 2020. IBM Support will work with any customers who already installed {{site.data.keyword.icp4dfull_notm}} 3.0.1 on Red Hat OpenShift 4.3. New customers who want to install on Red Hat OpenShift 4.x are instructed to install Red Hat OpenShift 4.5.
{: important}

See the following topics in the IBM Knowledge Center for the information that you need to get started with installation of the {{site.data.keyword.watson}} Speech services:

-   [Preparing the cluster for {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/knowledgecenter/SSQNUZ_3.0.1/cpd/svc/watson/text-to-speech-adm-cmd.html){: external}
-   [Override values for {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} installation](https://www.ibm.com/support/knowledgecenter/SSQNUZ_3.0.1/cpd/svc/watson/text-to-speech-override.html){: external}
-   [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/knowledgecenter/SSQNUZ_3.0.1/cpd/svc/watson/text-to-speech-install.html){: external}

See the following topic if you need to remove an installation:

-   [Uninstalling {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/knowledgecenter/SSQNUZ_3.0.1/cpd/svc/watson/text-to-speech-uninstall.html){: external}

## Where to continue
{: #speech-install-continue}

See the following pages for more information about installation and configuration parameters, and post-deployment management activities.

| Page | Contents |
|------|----------|
| [Using the override file](/docs/text-to-speech-data?topic=text-to-speech-data-speech-override) | Using values in the `speech-override.yaml` file to specify aspects of the installation and configuration that are common to both Speech services or are specific to {{site.data.keyword.speechtotextshort}} or {{site.data.keyword.texttospeechshort}}. |
| [Managing your cluster](/docs/text-to-speech-data?topic=text-to-speech-data-speech-cluster) | A collection of basic cluster and service management procedures and information. Topics include managing user access, using common cluster management commands, setting Red Hat OpenShift SecurityContextConstraints, disabling storage of user data, and installing ad hoc models and voices. |
| [Managing your datastores](/docs/text-to-speech-data?topic=text-to-speech-data-speech-datastores) | Administering the MinIO and PostgreSQL datastores. For MinIO, topics include security secrets, operation mode, and storage. For PostgreSQL, the page describes setting access credentials. |
| [Scaling up your installation](/docs/text-to-speech-data?topic=text-to-speech-data-speech-scaling) | Scaling from a development configuration to a production configuration. Topics include increasing the number of available CPUs for PostgreSQL and RabbitMQ, including the number of replicas for the Speech services and datastores. Topics also include setting the session-to-CPU ratio for the {{site.data.keyword.speechtotextshort}} runtime and customization AM patcher, and for the {{site.data.keyword.texttospeechshort}} runtime. |
| [Backing up and restoring your data](/docs/text-to-speech-data?topic=text-to-speech-data-speech-backup) | Backup and restore procedures for both disaster recovery and upgrade of your data. The procedures cover the MinIO and PostgreSQL datastores. |
{: caption="Table 1. Documentation overview and links"}
