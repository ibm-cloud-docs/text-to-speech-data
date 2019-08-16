---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-27"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 向服务提交请求
{: #making-requests}

要向 {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 提交认证请求，可供应服务实例并获取凭证。对服务的 HTTP 和 WebSocket 接口应该使用不同的 URL。如果使用自签名证书，那么需要禁用请求向服务进行 SSL 验证。
{: shortdesc}

## 供应实例并获取凭证
{: #making-requests-provisioning}

在使用 {{site.data.keyword.texttospeechshort}} 服务之前，必须供应服务实例并获取凭证。有关更多信息，请参阅[开始之前](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin)。在该过程的最后一步中，复制服务实例的 `{token}` 和 `{URL}`：

-   `{token}` 为您提供访问令牌以向服务进行认证。您可以使用 {{site.data.keyword.icp4dfull_notm}} Web 客户机中显示的访问令牌。但在生产环境中，要使用以编程方式生成的服务实例令牌。有关更多信息和示例，请参阅 [API 参考](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}中的*认证*。

    向 {{site.data.keyword.texttospeechshort}} 服务认证的方法是随每个请求传递访问令牌。{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 是一种多租户云解决方案。您的凭证仅提供对数据的访问权，而数据是与其他用户隔离开的。
-   `{URL}` 提供用于调用服务方法的基本端点。

URL 包含下列组件：

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

`{}`（花括号）中的变量值提供以下信息：

-   `{icp4d_cluster_host}` 是部署 {{site.data.keyword.icp4dfull_notm}} 集群的主机的名称或 IP 地址。
-   `{:port}` 是端口号，服务在该端口侦听指定主机上的请求。该端口号必须以 `:`（冒号）开头。
-   `{release}` 是发行版名称，该名称是在安装 Helm 图表时指定的。
-   `{instance_id}` 是服务实例的标识。

花括号指示必须替换为字面值的变量字符串。请勿在对服务的实际调用中包含花括号。
{: note}

## 发出认证 HTTP 请求
{: #httpRequest}

{{site.data.keyword.texttospeechshort}} 服务提供 [HTTP 接口](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP)，该接口提供对所有服务功能的访问，也包括定制接口。HTTP 接口接受通过 HTTP 安全协议发送的请求，而该协议又依赖于安全套接字层 (SSL)（或传输层安全性 (TLS)）协议。对 HTTP 接口的请求的所有 URL 都以 `https` 协议规范开头。

本文档中的示例使用 `curl` 命令来调用服务的 HTTP 接口。有关更多信息，请参阅[使用 curl 示例](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl)。带 `curl` 的 HTTP 请求的基本格式包含以下组件：

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

花括号中的变量值提供以下信息：

-   `{http_method}` 指定示例的 HTTP 请求方法：`POST`、`PUT`、`GET` 或 `DELETE`。除了 `GET` 以外的任何请求方法都必须有 `curl`。
-   `{token}` 提供服务实例的访问令牌。必须使用访问令牌才能向服务发出安全请求。
-   `{method}` 是您要调用的服务的方法。例如，使用 `synthesize` 方法向服务发出 HTTP 请求。

其余变量值提供先前描述的信息。很多方法的名称较长，并且包含必须作为请求组成部分指定的路径参数。大多数示例中还包含请求头、查询参数和其他值。

示例显示调用 HTTP 接口的 URL 为 `{url}/v1/{method}`。将 `{url}` 替换为刚才描述的值。
{: note}

## 发出认证 WebSocket 请求
{: #websocketRequest}

{{site.data.keyword.texttospeechshort}} 服务提供了一个 [WebSocket 接口](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket)，该接口仅提供语音合成。该服务接受通过 WebSocket 安全协议发送的请求，而该协议又依赖于安全套接字层 (SSL)（或传输层安全性 (TLS)）协议。对 WebSocket 接口的请求的所有 URL 都以 `wss` 协议规范开头。

只能从应用程序代码中调用 WebSocket 接口。不能从命令行调用 WebSocket 接口。您在以下端点位置建立了到服务的 WebSocket 连接。

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

该变量值提供先前描述的信息。您通过方法的 `access_token` 查询参数传递访问令牌。

示例显示调用 WebSocket 接口的 URL 为 `{ws_url}/v1/synthesize`。将 `{ws_url}` 替换为刚才描述的值。
{: note}

## 禁用 SSL 验证
{: #SSLverification}

所有 Watson 服务都使用 SSL（或 TLS）在客户机与服务器之间进行安全连接和通信。该连接会使用本地证书库进行验证，以确保认证、完整性和机密性。

{{site.data.keyword.icp4dfull_notm}} 安装自签名证书。缺省情况下，无法成功验证此证书。只要执行下列一项任务，即可成功连接到服务实例：

-   将自签名证书添加到用户代理的信任库。

    例如，要发出带 `curl` 的安全请求，请将证书添加到 `curl` 的信任库。要从浏览器发出安全请求，请将证书添加到浏览器的信任库。
-   禁用 SSL 验证。

    禁用 SSL 验证会削弱连接和数据安全性。强烈建议不要使用。仅当绝对必要时，再禁用 SSL，并要尽快执行步骤再启用 SSL。
    {: important}

    -   要对 `curl` 请求禁用 SSL 验证，请在请求中使用 `--insecure` (`-k`) 选项。此选项将引导命令绕过工具的 SSL 证书验证。
    -   要对 WebSocket 请求禁用 SSL 验证，请使用适合客户机库的方法，或使用某个 {{site.data.keyword.ibmwatson}} {{site.data.keyword.texttospeechshort}} SDK。

有关为对服务的调用禁用 SSL 验证的更多信息，请参阅 [API 参考](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}中的*禁用 SSL 验证*。该信息中包含 `curl` 以及所有 SDK 的示例。
