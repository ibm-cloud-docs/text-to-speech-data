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

# 정보
{: #about}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}에서는 작성된 텍스트를 자연어 음성으로 변환하여 애플리케이션에 필요한 음성 합성 기능을 제공합니다. 서비스는 지연을 최소로 하여 결과를 다시 클라이언트로 스트리밍합니다. 서비스는 [HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) 및 [WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) 인터페이스를 모두 제공합니다.

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} 설치 및 구성에 대한 정보는 [서비스 설치](/docs/services/text-to-speech-data?topic=text-to-speech-data-install)를 참조하십시오.

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}는 퍼블릭 {{site.data.keyword.cloud_notm}}의 {{site.data.keyword.texttospeechfull}} 서비스를 기반으로 합니다. 퍼블릭 서비스에 대한 자세한 정보는 [{{site.data.keyword.texttospeechshort}} 정보](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}를 참조하십시오.
{: note}

## 기능

{{site.data.keyword.texttospeechshort}} 서비스는 다음 기능을 제공합니다.

-   **오디오 형식** - Opus 또는 Vorbis 코덱, WAV, FLAC, MP3(MPEG), l16(PCM), mulaw 또는 기본 형식이 사용된 Ogg 또는 WebM에서 오디오를 생성합니다. 자세한 정보는 [오디오 형식](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats)을 참조하십시오.
-   **음성** - 다양한 언어, 음성 및 통용어로 텍스트-오디오 변환을 합성합니다. 자세한 정보는 [언어 및 음성](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices)을 참조하십시오.
-   **SSML** - 일반 텍스트 또는 XML 기반 SSML(Speech Synthesis Markup Language)로 표시되는 텍스트를 허용합니다. 자세한 정보는 [SSML 사용](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml)을 참조하십시오.
-   **단어 시간 지정** - WebSocket 인터페이스를 사용하여 입력 텍스트의 모든 문자열에 대해 SSML `<mark>` 요소 및 선택적인 단어 시간 지정 정보를 지원합니다. 시간 지정 정보는 입력 텍스트 및 생성되는 오디오를 동기화합니다. 자세한 정보는 [단어 시간 지정 가져오기](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing)를 참조하십시오.
-   **사용자 정의** - 서비스는 입력에서 발생하는 특이한 단어를 발음하는 방법을 지정하는 데 사용할 수 있는 사용자 정의 인터페이스를 제공합니다. IPA(International Phonetic Alphabet) 또는 {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation(SPR)을 사용하여 발음을 정의할 수 있습니다. 자세한 정보는 [사용자 정의 이해](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro)를 참조하십시오.

## 언어 지원
{: #languages-index}

서비스는 브라질 포르투갈어, 영어(영국 및 미국 통용어), 프랑스어, 독일어, 이탈리아어, 일본어 및 스페인어(카스티야어, 라틴 아메리카 및 북아메리카 통용어)로 음성을 지원합니다.

이 서비스에서는 언어마다 하나 이상의 여성 음성을 제공합니다. 이 서비스에서는 일부 언어용으로 남성과 여성 음성을 모두 포함하는 여러 음성을 제공합니다. 각 음성은 통용어에 적합한 운율 및 억양을 사용합니다.

각 언어에 사용할 수 있는 음성에 대한 자세한 정보는 [언어 및 음성](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices)을 참조하십시오.

일본어 음성은 보류 중이며 곧 사용할 수 있게 됩니다.
{: note}

## 유스 케이스
{: #usecases}

서비스는 오디오가 선호되는 출력 메소드인 음성 인식 및 화면 없는 애플리케이션에 적합합니다.

-   장애인을 위한 인터페이스(예: 시력이 손상된 사용자를 위한 지원 도구)
-   텍스트 및 이메일 메시지를 구동자에게 크게 읽어주기
-   동영상 스크립트 내래이션 및 동영상 음성
-   읽기 기반 교육 도구
-   가정 자동화 솔루션

## 서비스 사용

작동 중인 {{site.data.keyword.texttospeechshort}} 서비스의 예는 다음을 참조하십시오.

-   텍스트를 허용하고 다른 음성(voice)으로 음성(speech)을 생성하는 {{site.data.keyword.texttospeechshort}} 서비스의 [빠른 데모](https://text-to-speech-demo.ng.bluemix.net/){: external}입니다. 지원되는 경우 표현성(expressiveness) 및 변환(transformation)을 제공합니다.
-   {{site.data.keyword.texttospeechshort}} 서비스를 시연하는 {{site.data.keyword.ibmwatson}} [스타터 킷](http://www.ibm.com/watson/developercloud/starter-kits.html){: external}의 애플리케이션입니다.
