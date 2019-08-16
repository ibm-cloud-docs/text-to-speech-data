---

copyright:
  years: 2019
lastupdated: "2019-07-06"

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
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 關於
{: #about}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 為應用程式提供語音合成功能，可將書面文字轉換為自然語音。此服務會以最低延遲將結果串流回至用戶端。此服務同時提供 [HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) 及 [WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) 介面。

如需安裝和配置 {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 的資訊，請參閱[安裝服務](/docs/services/text-to-speech-data?topic=text-to-speech-data-install)。

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 是以公用 {{site.data.keyword.cloud_notm}} 上的 {{site.data.keyword.texttospeechfull}} 服務為基礎。如需公用服務的相關資訊，請參閱[關於 {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}。
{: note}

## 特性與功能

{{site.data.keyword.texttospeechshort}} 服務提供下列特性與功能：

-   **音訊格式** - 搭配使用 Ogg 或 WebM 與 Opus 或 Vorbis 轉碼器，或者使用 WAV、FLAC、MP3 (MPEG)、l16 (PCM)、mulaw 或基本格式來產生音訊。如需相關資訊，請參閱[音訊格式](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats)。
-   **語音** - 在各種語言、語音及用語中，將文字合成為音訊。如需相關資訊，請參閱[語言和語音](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices)。
-   **SSML** - 接受純文字或以 XML 型「語音合成標記語言 (SSML)」標註的文字。如需相關資訊，請參閱[使用 SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml)。
-   **字組計時** - 使用 WebSocket 介面，可支援 SSML `<mark>` 元素，以及輸入文字之所有字串的選用字組計時資訊。計時資訊會同步處理輸入文字及產生的音訊。如需相關資訊，請參閱[取得字組計時](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing)。
-   **自訂作業** - 提供一個自訂作業介面，您可以用來指定服務如何對輸入中出現的不尋常字組發音。您可以使用「國際音標 (IPA)」或「{{site.data.keyword.IBM_notm}} 符號語音表示法 (SPR)」來定義發音。如需相關資訊，請參閱[瞭解自訂作業](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro)。

## 語言支援
{: #languages-index}

此服務支援下列語言的語音：巴西葡萄牙文、英文（英式和美式用語）、法文、德文、義大利文、日文，以及西班牙文（卡斯提亞語、拉丁美洲及北美用語）。

服務針對每種語言至少提供一個女性語音。針對部分語言，服務提供多種語音，同時包括男性和女性語音。每種語音都會針對其用語使用適當的抑揚頓挫和語調。


如需每種語言可用之語音的相關資訊，請參閱[語言和語音](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices)。

日文語音目前擱置，不久即將可用。
{: note}

## 使用案例
{: #usecases}

服務適用於語音驅動及無螢幕的應用程式，在這些應用程式中，音訊是偏好的輸出方法：

-   適用於殘障人士的介面，例如視障者的協助工具
-   大聲閱讀寄至驅動程式的文字和電子郵件訊息
-   視訊 Script 旁白和視訊配音
-   閱讀型教育工具
-   首頁自動化解決方案

## 試用服務

如需動作中的 {{site.data.keyword.texttospeechshort}} 服務範例，請參閱：

-   {{site.data.keyword.texttospeechshort}} 服務的[快速示範](https://text-to-speech-demo.ng.bluemix.net/){: external}，此服務會接受文字，並產生不同的語音。它會提供支援的表達和轉換。
-   {{site.data.keyword.ibmwatson}} [入門範本套件](http://www.ibm.com/watson/developercloud/starter-kits.html){: external}中示範 {{site.data.keyword.texttospeechshort}} 服務的應用程式。
