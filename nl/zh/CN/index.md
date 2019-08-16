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

# 关于
{: #about}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 为应用程序提供语音合成功能，可将书面文本转换为自然语音。服务会以最短的延迟将结果流式返回给客户机。服务提供了 [HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) 和 [WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) 接口。

有关安装和配置 {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 的信息，请参阅[安装服务](/docs/services/text-to-speech-data?topic=text-to-speech-data-install)。

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} 基于公共 {{site.data.keyword.cloud_notm}} 上的 {{site.data.keyword.texttospeechfull}} 服务。有关公共服务的更多信息，请参阅[关于 {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}。
{: note}

## 特性和功能

{{site.data.keyword.texttospeechshort}} 服务提供了以下特性和功能：

-   **音频格式** - 生成以下格式的音频：Ogg 或 WebM（使用 Opus 或 Vorbis 编码解码器）、WAV、FLAC、MP3 (MPEG)、l16 (PCM)、mulaw 或基本格式。有关更多信息，请参阅[音频格式](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats)。
    
-   **声音** - 将文本合成为各种语言、声音和方言的音频。有关更多信息，请参阅[语言和声音](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices)。
-   **SSML** - 接受纯文本或使用基于 XML 的语音合成标记语言 (SSML) 标记的文本。有关更多信息，请参阅[使用 SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml)。
-   **词计时** - 使用 WebSocket 接口时，支持 SSML `<mark>` 元素以及输入文本中所有字符串的可选的词计时信息。计时信息可用于对输入文本和生成的音频进行同步。有关更多信息，请参阅[获取词计时](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing)。
-   **定制** - 提供了一个新的定制接口，可用于指定服务如何对输入中出现的异常词发音。可以使用国际音标 (IPA) 或 {{site.data.keyword.IBM_notm}} 符号拼音表示法 (SPR) 来定义发音。有关更多信息，请参阅[了解定制](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro)。
    

## 语言支持
{: #languages-index}

服务支持以下语言的声音：巴西葡萄牙语、英语（英国和美国方言）、法语、德语、意大利语、日语和西班牙语（卡斯蒂利亚、拉丁美洲和北美方言）。

对于每种语言，服务至少提供一个女声。对于某些语言，服务提供多个声音，同时包含男声和女声。每种声音会针对其方言使用相应的节奏和语调。


有关可用于每种语言的声音的更多信息，请参阅[语言和声音](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices)。

日语声音目前暂挂，不久即将可用。
{: note}

## 用例
{: #usecases}

服务适用于声音驱动和无屏幕应用程序，其中音频是输出的首选方法：

-   针对残障人士的界面，例如面向视力受损人士的辅助工具
-   向驾驶员朗读文本和电子邮件消息
-   视频脚本叙述和视频话外音
-   基于朗读的教育工具
-   家庭自动化解决方案

## 试用服务

有关运行中 {{site.data.keyword.texttospeechshort}} 服务的示例，请参阅：

-   {{site.data.keyword.texttospeechshort}} 服务的[快速演示](https://text-to-speech-demo.ng.bluemix.net/){: external}，用于演示接受文本并生成具有不同声音的语音。它在支持的情况下提供了表现力和变换。
-   {{site.data.keyword.ibmwatson}} [入门模板工具包](http://www.ibm.com/watson/developercloud/starter-kits.html){: external}中的应用程序，用于演示 {{site.data.keyword.texttospeechshort}} 服务。
