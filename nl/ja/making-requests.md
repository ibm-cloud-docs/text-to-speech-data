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

# サービスに対する要求の発行
{: #making-requests}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} に対して認証済みの要求を行うには、サービスのインスタンスをプロビジョンし、資格情報を取得する必要があります。サービスの HTTP インターフェースと WebSocket インターフェースとで、それぞれ異なる URL を使用します。自己署名証明書を使用する場合は、サービスに対する要求の SSL 検証を無効にする必要があります。
{: shortdesc}

## インスタンスのプロビジョニングと資格情報の取得
{: #making-requests-provisioning}

{{site.data.keyword.texttospeechshort}} サービスを使用する前に、サービスのインスタンスをプロビジョンし、資格情報を取得する必要があります。詳しくは、[始めに](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin)を参照してください。手順の最後のステップで、サービス・インスタンスの `{token}` と `{URL}` をコピーします。

-   `{token}` は、サービスに対する認証に使用されるアクセス・トークンを示します。{{site.data.keyword.icp4dfull_notm}} Web クライアントに表示されるアクセス・トークンを使用できます。ただし、実稼働環境では、サービス・インスタンス用にプログラムで生成するトークンを使用してください。詳細情報と例については、[API リファレンス](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}の*認証* を参照してください。

要求ごとにアクセス・トークンを渡すことによって、{{site.data.keyword.texttospeechshort}} に対して認証が行われます。{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} はマルチテナント・クラウド・ソリューションです。資格情報によって自身のデータに対するアクセス権限のみが付与され、自身のデータは他のユーザーから分離されています。
-   `{URL}` は、サービスのメソッドを呼び出すために使用する基本エンドポイントを示します。

URL には、以下の構成要素が含まれます。

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

`{}` (中括弧) 内の可変値は、以下の情報を示します。

-   `{icp4d_cluster_host}` は、{{site.data.keyword.icp4dfull_notm}} クラスターがデプロイされているホストの名前または IP アドレスです。
-   `{:port}` は、指定されたホスト上でサービスが要求を listen するポート番号です。ポート番号の前に `:` (コロン) を付ける必要があります。
-   `{release}` は、Helm チャートがインストールされたときに指定されたリリース名です。
-   `{instance_id}` は、サービス・インスタンスの ID です。

中括弧は、リテラル値に置き換える必要がある可変ストリングを示しています。実際のサービス呼び出しでは中括弧を含めないでください。
{: note}

## 認証対象の HTTP 要求の発行
{: #httpRequest}

{{site.data.keyword.texttospeechshort}} サービスには、カスタマイズ・インターフェースを含むサービスの機能全体にアクセスできる [HTTP インターフェース](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP)があります。HTTP インターフェースは HTTP Secure プロトコルを介して要求を受け入れ、その HTTP セキュア・プロトコルは Secure Sockets Layer (SSL) (または Transport Layer Security (TLS)) プロトコルを使用します。HTTP インターフェースに対する要求の URL はすべて、`https` プロトコル指定で始まります。

本資料の例では、`curl` コマンドを使用して、サービスの HTTP インターフェースを呼び出します。詳しくは、[curl の使用例](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl)を参照してください。`curl` を使用した HTTP 要求の基本フォーマットには、以下の構成要素が含まれます。

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

中括弧内の可変値は、以下の情報を示します。

-   `{http_method}` は、HTTP 要求メソッドを指定します (例えば、`POST`、`PUT`、`GET`、`DELETE`)。`curl` では `GET` 以外の場合は要求メソッドは必須です。
-   `{token}` は、サービス・インスタンスのアクセス・トークンを示します。サービスに対してセキュア要求を行うには、アクセス・トークンを使用する必要があります。
-   `{method}` は、呼び出すサービスのメソッドです。例えば、`synthesize` メソッドを使用して、サービスに対して HTTP 要求を行います。

残りの可変値は、前述の情報を示します。多くのメソッドは名前が長く、要求の一部として指定する必要があるパス・パラメーターを含んでいます。また、ほとんどの例に、要求ヘッダーや照会パラメーターなどの値が含まれています。

例では、HTTP インターフェースに対する呼び出しのための URL を `{url}/v1/{method}` と示しています。`{url}` を、先ほど述べた値に置き換えてください。
{: note}

## 認証対象の WebSocket 要求の発行
{: #websocketRequest}

{{site.data.keyword.texttospeechshort}} サービスには、音声合成のみを提供する [WebSocket インターフェース](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket)があります。サービスは WebSocket Secure プロトコルを介して要求を受け入れ、WebSocket セキュア・プロトコルもまた、Secure Sockets Layer (SSL) (または Transport Layer Security (TLS)) プロトコルを使用します。WebSocket インターフェースに対する要求の URL はすべて、`wss` プロトコル指定で始まります。

WebSocket インターフェースは、アプリケーション・コードからのみ呼び出せます。コマンド・ラインから WebSocket インターフェースを呼び出すことはできません。次のエンドポイントでサービスへの WebSocket 接続を確立します。

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

可変値は、前述の情報を示します。メソッドの `access_token` 照会パラメーターを介してアクセス・トークンを渡します。

例では、WebSocket インターフェースに対する呼び出しのための URL を `{ws_url}/v1/synthesize` と示しています。`{ws_url}` を、先ほど述べた値に置き換えてください。
{: note}

## SSL 検証の無効化
{: #SSLverification}

Watson サービスはすべて、クライアントとサーバーの間のセキュアな接続と通信に SSL (または TLS) を使用します。認証、保全性、機密性を裏付けるために、ローカル証明書ストアに照らして接続が検証されます。

{{site.data.keyword.icp4dfull_notm}} によって自己署名証明書がインストールされます。デフォルトでは、この証明書を正常に検証することはできません。サービス・インスタンスに正常に接続するには、以下のいずれかを実行します。

-   ユーザー・エージェントのトラストストアに自己署名証明書を追加します。

    例えば、`curl` を使用してセキュア要求を行うには、`curl` のトラストストアに証明書を追加します。ブラウザーからセキュア要求を行うには、ブラウザーのトラストストアに証明書を追加します。
-   SSL 検証を無効にします。

    SSL 検証を無効にすると、接続とデータのセキュリティーが損なわれます。この方法を使用しないことを強くお勧めします。どうしても必要な場合だけ SSL を無効にし、SSL を有効にするステップをできるだけ早く実行してください。
    {: important}

    -   `curl` 要求の SSL 検証を無効にするには、要求で `--insecure` (`-k`) オプションを使用します。このオプションは、ツールによる SSL 証明書検証をバイパスするようコマンドに指示します。
    -   WebSocket 要求の SSL 検証を無効にするには、ご使用のクライアント・ライブラリーに対応したアプローチを使用するか、いずれかの {{site.data.keyword.ibmwatson}} {{site.data.keyword.texttospeechshort}} SDK を使用します。

サービス呼び出しの SSL 検証の無効化について詳しくは、[API リファレンス](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}の *SSL 検証の無効化*を参照してください。そこには、`curl` の例とすべての SDK の例が含まれています。
