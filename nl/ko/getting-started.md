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

# 시작하기 튜토리얼
{: #gettingStarted}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}는 작성된 텍스트를 자연어 음성으로 변환하여 애플리케이션에 필요한 음성 합성 기능을 제공합니다. 이 curl 기반 튜토리얼은 서비스를 빠르게 시작하는 데 도움을 줍니다. 예에서는 오디오 스트림을 요청하기 위해 서비스의 `POST` 및 `GET /v1/synthesize` 메소드를 호출하는 방법을 보여줍니다.
{: shortdesc}

## 시작하기 전에
{: #before-you-begin}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}를 사용하려면 다음 단계를 완료해야 합니다.

1.  {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}의 인스턴스를 프로비저닝하십시오. 프로비저닝에 대한 자세한 정보는 [서비스 설치](/docs/services/text-to-speech-data?topic=text-to-speech-data-install)를 참조하십시오.
1.  {{site.data.keyword.icp4dfull_notm}} 웹 클라이언트 메뉴에서 **내 인스턴스**를 선택하십시오.
1.  {{site.data.keyword.texttospeechshort}} 인스턴스를 클릭하여 개요 페이지를 여십시오. `{token}` 및 `{URL}` 인증 정보 값을 복사하십시오.

### curl 예제 사용
{: #getting-started-curl}

이 튜토리얼에서는 `curl` 명령을 사용하여 서비스 HTTP 인터페이스의 메소드를 호출합니다. 시스템에 `curl` 명령이 설치되어 있는지 확인하십시오.

1.  `curl` 설치 여부를 테스트하려면 명령행에서 다음 명령을 실행하십시오. 출력에서 SSL(Secure Socket Layer)을 지원하는 `curl` 버전을 나열하면 튜토리얼이 준비된 것입니다.

    ```bash
    curl -V
    ```
    {: pre}

1.  필요한 경우 [curl.haxx.se](https://curl.haxx.se/){: external}에서 사용자 운영 체제용으로 SSL이 사용 설정된 `curl` 버전을 설치하십시오.

예에서 중괄호를 생략하십시오. 중괄호는 변수값을 나타냅니다.
{: tip}

## 1단계: 미국 영어로 된 텍스트 합성
{: #synthesizeEnglish}

다음 명령에서는 `POST /v1/synthesize` 메소드를 사용하여 두 가지 다른 형식으로 미국 영어 입력을 오디오 파일로 합성합니다. 두 요청에서는 기본적으로 미국 영어 음성(`en-US_MichaelVoice`)을 사용합니다.

1.  다음 명령을 실행하여 문자열 "hello world"를 합성하고 `hello_world.wav`라는 이름으로 WAV 파일을 생성하십시오.
    -   `{token}`을 사용자의 서비스 인스턴스의 액세스 토큰으로 바꾸십시오.
    -   `{url}`을 사용자의 서비스 인스턴스의 URL로 바꾸십시오.

    *Windows 사용자*의 경우 각 행의 끝에서 백슬래시(``\`)를 캐럿(``^`)으로 바꾸십시오. 후미에 공백을 두지 마십시오.
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

1.  다음 명령을 실행하여 동일한 텍스트를 합성하지만 `hello_world.ogg`라는 Ogg 파일(기본 형식)을 생성하십시오.
    -   `{token}`을 사용자의 서비스 인스턴스의 액세스 토큰으로 바꾸십시오.
    -   `{url}`을 사용자의 서비스 인스턴스의 URL로 바꾸십시오.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"
    ```
    {: pre}

브라우저 또는 기타 도구를 사용하여 예를 통해 생성된 오디오 파일을 재생할 수 있습니다. 자세한 정보는 [오디오 파일 재생](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats#formatsPlay)을 참조하십시오.
{: note}

## 2단계: 스페인어로 된 텍스트 합성
{: #synthesizeSpanish}

다음 명령에서는 `GET /v1/synthesize` 메소드를 사용하여 스페인어 입력을 오디오 파일로 합성합니다.

1.  다음 명령을 실행하여 문자열 "hola mundo"를 합성하고 `hola_mundo.wav`라는 이름으로 WAV 파일을 생성하십시오. 입력 텍스트는 URL 인코딩입니다. 메소드는 조회 매개변수 `accept`를 포함하여 오디오 형식을 지정하고 `voice`를 포함하여 스페인어 음성(`es-ES_EnriqueV3Voice`)을 지정합니다.
    -   `{token}`을 사용자의 서비스 인스턴스의 액세스 토큰으로 바꾸십시오.
    -   `{url}`을 사용자의 서비스 인스턴스의 URL로 바꾸십시오.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

## 다음 단계

-   [HTTP 인터페이스](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP)에서 서비스의 HTTP 인터페이스에 대해 알아보십시오.
-   [WebSocket 인터페이스](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket)에서 서비스의 WebSocket 인터페이스에 대해 알아보십시오.
-   [API 참조](https://{DomainName}/apidocs/text-to-speech-data){: external}에서 서비스 인터페이스의 모든 메소드에 관한 자세한 정보를 찾으십시오.
