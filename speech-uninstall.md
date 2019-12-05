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

# Uninstalling the Watson Text to Speech add-on
{: #tts-uninstalling}

You can uninstall the {{site.data.keyword.texttospeechdatafull}} add-on from {{site.data.keyword.icp4dfull}}.
{: shortdesc}

## Uninstalling the add-on
{: #uninstall}

To uninstall and delete the `{release-name}` Helm release, run the following command:

```sh
helm delete --tls {release-name}
```

To irrevocably uninstall and delete the `{release-name}` Helm release, run the following command:

```sh
helm delete --purge --tls {release-name}
```

If you omit the `--purge` option, Helm deletes all resources for the deployment but retains the record with the release name. This allows you to roll back the deletion. If you include the `--purge` option, Helm removes all records for the deployment so that the name can be used for another installation.