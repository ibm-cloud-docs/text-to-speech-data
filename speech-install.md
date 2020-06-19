---

copyright:
  years: 2019, 2020
lastupdated: "2020-06-19"

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
{:download: .download}
{:gif: data-image-type='gif'}

# Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} version 1.1.4
{: #speech-install}

This and the following pages provide information about installing and managing {{site.data.keyword.speechtotextdatafull}} and {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}. The two services share a common installation and common datastores to allow for more efficient resource consumption and simplified support. Most of the installation information therefore applies to both services.
{: shortdesc}

The following pages often refer to the combination of {{site.data.keyword.speechtotextshort}} and {{site.data.keyword.texttospeechshort}} as *Speech services.* Information specific to just one of the two services is clearly identified.
{: note}

## Where to begin
{: #speech-install-begin}

See the following topics in the IBM Knowledge Center for the information that you need to get started with installation of the {{site.data.keyword.watson}} Speech services:

-   [Preparing the cluster for {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/watson/text-to-speech-adm-cmd.html)
-   [Override values for {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}} installation](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/watson/text-to-speech-override.html)
-   [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/watson/text-to-speech-install.html)

See the following topic if you need to remove an installation:

-   [Uninstalling {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/cpd/svc/watson/text-to-speech-uninstall.html)

## Where to continue
{: #speech-install-continue}

See the following pages for more information about installation and configuration parameters, and post-deployment management activities.

<table>
  <caption>Table 1. Documentation overview and links</caption>
  <tr>
    <th>
      Page
    </th>
    <th>
      Contents
    </th>
  </tr>
  <tr>
    <td>
      [Using the override file](/docs/text-to-speech-data?topic=text-to-speech-data-speech-override)
    </td>
    <td>
      Using values in the `speech-override.yaml` file to specify aspects
      of the installation and configuration that are common to both Speech
      services or are specific to {{site.data.keyword.speechtotextshort}}
      or {{site.data.keyword.texttospeechshort}}.
    </td>
  </tr>
  <tr>
    <td>
      [Managing your datastores](/docs/text-to-speech-data?topic=text-to-speech-data-speech-datastores)
    </td>
    <td>
      Administering the Minio and PostgreSQL datastores. For Minio, topics
      include security secrets, operation mode, and storage. For PostgreSQL,
      the page describes setting access credentials.
    </td>
  </tr>
  <tr>
    <td>
      [Managing your cluster](/docs/text-to-speech-data?topic=text-to-speech-data-speech-cluster)
    </td>
    <td>
      A collection of basic cluster and service management procedures and
      information. Topics include managing user access, using common cluster
      management commands, setting Red Hat OpenShift
      SecurityContextConstraints, disabling storage of user data, and
      installing ad hoc models and voices.
    </td>
  </tr>
  <tr>
    <td>
      [Scaling up your installation](/docs/text-to-speech-data?topic=text-to-speech-data-speech-scaling)
    </td>
    <td>
      Scaling from a development configuration to a production configuration.
      Topics include increasing the number of available CPUs for PostgreSQL
      and RabbitMQ, including the number of replicas for the Speech services
      and datastores. Topics also include setting the session-to-CPU ratio
      for the {{site.data.keyword.speechtotextshort}} runtime and
      customization AM patcher, and for the
      {{site.data.keyword.texttospeechshort}} runtime.
    </td>
  </tr>
  <tr>
    <td>
      [Backing up and restoring your data](/docs/text-to-speech-data?topic=text-to-speech-data-speech-backup)
    </td>
    <td>
      Backup and restore procedures for both disaster recovery and upgrade
      of your data. The procedures cover the Minio and PostgreSQL datastores.
    </td>
  </tr>
</table>
