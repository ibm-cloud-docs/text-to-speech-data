---

copyright:
  years: 2019, 2020
lastupdated: "2020-02-04"

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

# Making requests to the service
{: #making-requests}

To make authenticated requests to {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}, you provision an instance of the service and obtain credentials. You use a different URL for the service's HTTP and WebSocket interfaces. If you use a self-signed certificate, you need to disable SSL verification for requests to the service.
{: shortdesc}

## Provisioning an instance and obtaining credentials
{: #making-requests-provisioning}

Before using the {{site.data.keyword.texttospeechshort}} service, you must provision an instance of the service and obtain your credentials. For more information, see [Before you begin](/docs/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin). In the last step of that procedure, you copy the `{token}` and `{URL}` for your service instance:

-   The `{token}` provides your access token for authenticating to the service. You can use the access token displayed in the {{site.data.keyword.icp4dfull_notm}} web client. However, in a production environment, use a token that you generate programmatically for your service instance. For more information and for examples, see *Authentication* in the [API reference](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}.

    You authenticate to the {{site.data.keyword.texttospeechshort}} service by passing your access token with each request. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} is a multi-tenant cloud solution. Your credentials provide access only to your data, and your data is isolated from other users.
-   The `{URL}` provides the base endpoint that you use to call methods of the service.

The URL contains the following components:

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

The variable values in `{}` (braces) provide the following information:

-   `{icp4d_cluster_host}` is the name or IP address of the host on which your {{site.data.keyword.icp4dfull_notm}} cluster is deployed.
-   `{:port}` is the port number at which the service listens for requests on the specified host. You must precede the port number with a `:` (colon).
-   `{release}` is the release name that was specified when the Helm chart was installed.
-   `{instance_id}` is the identifier of your service instance.

The braces indicate variable strings that you must replace with literal values. Do not include the braces in actual calls to the service.
{: note}

## Making an authenticated HTTP request
{: #httpRequest}

The {{site.data.keyword.texttospeechshort}} service offers an [HTTP interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingHTTP) that provides access to all of the service's functionality, including the customization interfaces. The HTTP interface accepts requests over the HTTP Secure protocol, which in turn relies on the Secure Sockets Layer (SSL) (or Transport Layer Security (TLS)) protocol. All URLs for requests to the HTTP interface begin with the `https` protocol specification.

The examples in this documentation use the `curl` command to call the service's HTTP interface. For more information, see [Using the curl examples](/docs/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl). The basic format of an HTTP request with `curl` includes the following components:

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

The variable values in braces provide the following information:

-   `{http_method}` specifies the HTTP request method for the example: `POST`, `PUT`, `GET`, or `DELETE`. The request method is required with `curl` for anything other than `GET`.
-   `{token}` provides the access token for your service instance. You must use the access token to make a secure request to the service.
-   `{method}` is the method of the service that you are calling. For example, you use the `synthesize` method to make an HTTP request to the service.

The remaining variable values provide the information that was described previously. Many methods have longer names and include path parameters that you must specify as part of the request. Most examples also include request headers, query parameters, and other values.

The examples show the URL for calls to the HTTP interface as `{url}/v1/{method}`. Replace `{url}` with the values just described.
{: note}

## Making an authenticated WebSocket request
{: #websocketRequest}

The {{site.data.keyword.texttospeechshort}} service offers a [WebSocket interface](/docs/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) that provides only speech synthesis. The service accepts requests over the WebSocket Secure protocol, which again relies on the Secure Sockets Layer (SSL) (or Transport Layer Security (TLS)) protocol. All URLs for requests to the WebSocket interface begin with the `wss` protocol specification.

You can call the WebSocket interface only from application code. You cannot call the WebSocket interface from the command line. You establish a WebSocket connection to the service at the following endpoint.

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

The variable values provide the information that was described previously. You pass your access token via the method's `access_token` query parameter.

The examples show the URL for calls to the WebSocket interface as `{ws_url}/v1/synthesize`. Replace `{ws_url}` with the values just described.
{: note}

## Disabling SSL verification
{: #SSLverification}

All Watson services use SSL (or TLS) for secure connections and communications between the client and server. The connection is verified against the local certificate store to ensure authentication, integrity, and confidentiality.

{{site.data.keyword.icp4dfull_notm}} installs a self-signed certificate. This certificate cannot be successfully verified by default. You can do one of the following to successfully connect to a service instance:

-   Add the self-signed certificate to the truststore for your user agent.

    For example, to make secure requests with `curl`, add the certificate to the truststore for `curl`. To make secure requests from your browser, add the certificate to the truststore for the browser.
-   Disable SSL verification.

    Disabling SSL verification compromises the security of the connection and data. It is highly discouraged. Disable SSL only if absolutely necessary, and take steps to enable SSL as soon as possible.
    {: important}

    -   To disable SSL verification for a `curl` request, use the `--insecure` (`-k`) option with the request. This option directs the command to bypass the tool's verification of SSL certificates.
    -   To disable SSL verification for a WebSocket request, use the appropriate approach for your client library or use one of the {{site.data.keyword.ibmwatson}} {{site.data.keyword.texttospeechshort}} SDKs.

For more information about disabling SSL verification for calls to the service, see *Disabling SSL verification* in the [API reference](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}. The information includes examples for `curl` and for all of the SDKs.
