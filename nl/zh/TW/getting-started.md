---

copyright:
  years: 2019
lastupdated: "2019-07-30"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# 入門指導教學
{: #gettingStarted}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 將書面文字轉換為自然發音的語音，以便為應用程式提供語音合成功能。這個 curl 型指導教學可協助您快速開始使用服務。範例顯示如何呼叫服務的 `POST` 和 `GET /v1/synthesize` 方法來要求音訊串流。
{: shortdesc}

## 開始之前
{: #before-you-begin}

若要使用 {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}，必須先完成下列步驟：

1.  佈建 {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 的實例。如需佈建的相關資訊，請參閱[安裝服務](/docs/services/text-to-speech-data?topic=text-to-speech-data-install)。
1.  在 {{site.data.keyword.icp4dfull_notm}} Web 用戶端功能表中，選擇**我的實例**。
1.  按一下 {{site.data.keyword.texttospeechshort}} 實例以開啟概觀頁面。複製 `{token}` 和 `{URL}` 認證值。

### 使用 curl 範例
{: #getting-started-curl}

本指導教學使用 `curl` 指令來呼叫服務的 HTTP 介面的方法。確保您的系統上已安裝 `curl` 指令。

1.  若要測試是否已安裝 `curl`，請在指令行上執行下列指令。如果輸出中列出了支援 Secure Sockets Layer (SSL) 的 `curl` 版本，則已設定好進行指導教學。

    ```bash
    curl -V
    ```
    {: pre}

1.  必要的話，請從 [curl.haxx.se](https://curl.haxx.se/){: external} 安裝適合您作業系統並且已啟用 SSL 的 `curl` 版本。

請省略範例中的大括弧。大括弧用於指示變數值。
{: tip}

## 步驟 1：合成美式英文的文字
{: #synthesizeEnglish}

下列指令使用 `POST /v1/syntheize` 方法，以兩種不同格式將美式英文輸入合成為音訊檔。這兩個要求皆會使用預設美式英文語音 `en-US_MichaelVoice`。

1.  發出下列指令來合成 "hello world" 字串，並產生名稱為 `hello_world.wav` 的 WAV 檔案。
    -   將 `{token}` 取代為服務實例的存取記號。
    -   將 `{url}` 取代為服務實例的 URL。

    *Windows 使用者，*將每行結尾的反斜線 (`\`) 取代為脫字符號 (`^`)。請確定沒有尾端空格。
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"
    ```
    {: pre}

1.  發出下列指令來合成相同文字，但產生名稱為 `hello_world.ogg` 的 Ogg 檔（預設格式）。
    -   將 `{token}` 取代為服務實例的存取記號。
    -   將 `{url}` 取代為服務實例的 URL。

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"
    ```
    {: pre}

可以使用瀏覽器或其他工具來播放範例所產生的音訊檔案。如需相關資訊，請參閱[播放音訊檔](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats#formatsPlay)。
{: note}

## 步驟 2：合成西班牙文的文字
{: #synthesizeSpanish}

下列指令使用 `GET /v1/synthesize` 方法，將西班牙文輸入合成為音訊檔。

1.  發出下列指令來合成 "hola mundo" 字串，並產生名稱為 `hola_mundo.wav` 的 WAV 檔案。輸入文字是 URL 編碼文字。此方法包括查詢參數 `accept` 以指定音訊格式，以及查詢參數 `voice` 以指定西班牙文語音 `es-ES_EnriqueV3Voice`。
    -   將 `{token}` 取代為服務實例的存取記號。
    -   將 `{url}` 取代為服務實例的 URL。

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

## 後續步驟

-   在 [HTTP 介面](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP)中進一步瞭解服務的 HTTP 介面。
-   在 [WebSocket 介面](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket)中瞭解服務的 WebSocket 介面。
-   在 [API 參考資料](https://{DomainName}/apidocs/text-to-speech-data){: external}中獲取有關所有服務介面方法的詳細資料。
