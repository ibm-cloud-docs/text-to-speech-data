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

# 向服務提交要求
{: #making-requests}

若要向 {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 提交鑑別要求，可佈建服務實例並取得認證。對服務的 HTTP 和 WebSocket 介面應該使用不同的 URL。如果使用自簽憑證，則需要停用要求向服務進行 SSL 驗證。
{: shortdesc}

## 佈建實例並取得認證
{: #making-requests-provisioning}

在使用 {{site.data.keyword.texttospeechshort}} 服務之前，必須佈建服務實例並取得認證。如需相關資訊，請參閱[開始之前](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin)。在該程序的最後一個步驟中，複製服務實例的 `{token}` 和 `{URL}`：

-   `{token}` 為您提供存取記號以向服務進行鑑別。您可以使用 {{site.data.keyword.icp4dfull_notm}} Web 用戶端中顯示的存取記號。但在正式作業環境中，請使用以程式設計方式產生的服務實例記號。如需相關資訊和範例，請參閱 [API 參考資料](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}中的*鑑別*。

    向 {{site.data.keyword.texttospeechshort}} 服務鑑別的方法是隨每個要求傳遞存取記號。{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 是多方承租戶雲端解決方案。您的認證只提供對您資料的存取權，您的資料會與其他使用者隔離。
-   `{URL}` 提供用於呼叫服務方法的基礎端點。

URL 包含下列元件：

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

`{}`（大括弧）中的變數值提供下列資訊：

-   `{icp4d_cluster_host}` 是部署 {{site.data.keyword.icp4dfull_notm}} 叢集的主機的名稱或 IP 位址。
-   `{:port}` 是服務接聽指定主機上要求的埠號。該埠號必須以 `:`（冒號）開頭。
-   `{release}` 是版本名稱，該名稱是在安裝 Helm Chart 時指定。
-   `{instance_id}` 是服務實例的 ID。

大括弧指示必須取代為文字值的變數字串。請勿在對服務的實際呼叫中包含大括弧。
{: note}

## 發出鑑別 HTTP 要求
{: #httpRequest}

{{site.data.keyword.texttospeechshort}} 服務提供 [HTTP 介面](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP)，該介面提供對所有服務功能的存取，也包括自訂作業介面。HTTP 介面接受透過 HTTP 安全通訊協定傳送的要求，而該通訊協定又依賴 Secure Sockets Layer (SSL)（或傳輸層安全 (TLS)）通訊協定。對 HTTP 介面之要求的所有 URL 都以 `https` 通訊協定規格開頭。

本文件中的範例使用 `curl` 指令來呼叫服務的 HTTP 介面。如需相關資訊，請參閱[使用 curl 範例](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl)。使用 `curl` 的 HTTP 要求基本格式包含下列元件：

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

大括弧中的變數值提供下列資訊：

-   `{http_method}` 指定範例的 HTTP 要求方法：`POST`、`PUT`、`GET` 或 `DELETE`。除了 `GET` 以外的任何要求方法都必須有 `curl`。
-   `{token}` 提供服務實例的存取記號。必須使用存取記號才能向服務發出安全要求。
-   `{method}` 是您要呼叫的服務的方法。例如，使用 `synthesize` 方法向服務發出 HTTP 要求。

其餘變數值提供先前說明的資訊。很多方法的名稱較長，並且包含路徑參數，您必須將這些參數指定為要求的一部分。大部分的範例還包含要求標頭、查詢參數和其他值。

範例顯示呼叫 HTTP 介面的 URL 為 `{url}/v1/{method}`。將 `{url}` 取代為剛才說明的值。
{: note}

## 發出鑑別 WebSocket 要求
{: #websocketRequest}

{{site.data.keyword.texttospeechshort}} 服務提供了一個 [WebSocket 介面](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket)，該介面僅提供語音合成。該服務接受透過 WebSocket 安全通訊協定傳送的要求，而該通訊協定又依賴 Secure Sockets Layer (SSL)（或傳輸層安全 (TLS)）通訊協定。對 WebSocket 介面之要求的所有 URL 都以 `wss` 通訊協定規格開頭。

只能從應用程式碼中呼叫 WebSocket 介面。不能從指令行呼叫 WebSocket 介面。您在下列端點位置建立 WebSocket 與服務的連線。

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

該變數值提供先前說明的資訊。您藉由方法的 `access_token` 查詢參數傳遞存取記號。

範例顯示呼叫 WebSocket 介面的 URL 為 `{ws_url}/v1/synthesize`。將 `{ws_url}` 取代為剛才說明的值。
{: note}

## 停用 SSL 驗證
{: #SSLverification}

所有 Watson 服務都使用 SSL（或 TLS）在用戶端與伺服器之間進行安全連線和通訊。該連線會使用本端憑證儲存庫進行驗證，以確保鑑別、完整性和機密性。

{{site.data.keyword.icp4dfull_notm}} 安裝自簽憑證。依預設，無法順利驗證此憑證。只要執行下列一項任務，即可順利連接至服務實例：

-   將自簽憑證新增到使用者代理程式的信任儲存庫。

    例如，要發出具有 `curl` 的安全要求，請將憑證新增到 `curl` 的信任儲存庫。若要從瀏覽器發出安全要求，請將憑證新增到瀏覽器的信任儲存庫。
-   停用 SSL 驗證。

    停用 SSL 驗證會危及連線和資料安全。強烈建議不要使用。僅當絕對必要時，再停用 SSL，並要盡快採取步驟再啟用 SSL。
    {: important}

    -   若要對 `curl` 要求停用 SSL 驗證，請在要求中使用 `--insecure` (`-k`) 選項。此選項將引導指令繞過工具的 SSL 憑證驗證。
    -   若要對 WebSocket 要求停用 SSL 驗證，請使用適合用戶端程式庫的方法，或使用某個 {{site.data.keyword.ibmwatson}} {{site.data.keyword.texttospeechshort}} SDK。

如需針對服務呼叫停用 SSL 驗證的相關資訊，請參閱 [API 參考資料](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}中的*停用 SSL 驗證*。該資訊中包含 `curl` 以及所有 SDK 的範例。
