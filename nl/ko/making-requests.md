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

# 서비스에 대한 요청 작성
{: #making-requests}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}에 인증된 요청을 작성하기 위해 서비스의 인스턴스를 프로비저닝하고 인증 정보를 얻습니다. 서비스의 HTTP 및 WebSocket 인터페이스에 대해 다른 URL을 사용합니다. 자체 서명된 인증서를 사용하는 경우, 서비스에 대한 요청에 대해 SSL 검증을 사용하지 않도록 설정해야 합니다.
{: shortdesc}

## 인스턴스 프로비저닝 및 인증 정보 얻기
{: #making-requests-provisioning}

{{site.data.keyword.texttospeechshort}} 서비스를 사용하기 전에 서비스의 인스턴스를 프로비저닝하고 인증 정보를 얻어야 합니다. 자세한 정보는 [시작하기 전에](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin)를 참조하십시오. 해당 프로시저의 마지막 단계에서 사용자의 서비스 인스턴스에 대한 `{token}` 및 `{URL}`을 복사합니다.

-   `{token}`은 서비스 인증에 필요한 액세스 토큰을 제공합니다. {{site.data.keyword.icp4dfull_notm}} 웹 클라이언트에 표시되는 액세스 토큰을 사용할 수 있습니다. 단, 프로덕션 환경에서는 서비스 인스턴스에 대해 프로그래밍 방식으로 생성되는 토큰을 사용하십시오. 자세한 정보 및 예는 [API 참조](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}에서 *인증*을 참조하십시오.

    각 요청과 함께 액세스 토큰을 전달하여 {{site.data.keyword.texttospeechshort}} 서비스에 대해 인증을 수행합니다. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}는 다중 테넌트 클라우드 솔루션입니다. 사용자의 인증 정보는 사용자의 데이터에 대한 액세스만 제공하며 사용자의 데이터는 다른 사용자로부터 격리됩니다.
-   `{URL}`은 서비스의 메소드를 호출하는 데 사용하는 기본 엔드포인트를 제공합니다.

URL은 다음 컴포넌트를 포함합니다.

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

`{}`(중괄호) 내의 변수값은 다음 정보를 제공합니다.

-   `{icp4d_cluster_host}`는 사용자의 {{site.data.keyword.icp4dfull_notm}} 클러스터가 배치되는 호스트의 이름 또는 IP 주소입니다.
-   `{:port}`는 지정된 호스트에서 서비스가 요청을 청취하는 포트 번호입니다. `:`(콜론)이 포트 번호 앞에 와야 합니다.
-   `{release}`는 Helm 차트가 설치될 때 지정된 릴리스 이름입니다.
-   `{instance_id}`는 서비스 인스턴스의 ID입니다.

중괄호는 리터럴 값으로 대체해야 하는 변수 문자열을 표시합니다. 서비스에 대한 실제 호출에 중괄호를 포함시키지 마십시오.
{: note}

## 인증된 HTTP 요청 작성
{: #httpRequest}

{{site.data.keyword.texttospeechshort}} 서비스는 인터페이스 사용자 정의를 포함하여 서비스의 모든 기능에 대한 액세스를 제공하는 [HTTP 인터페이스](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP)를 제공합니다. HTTP 인터페이스는 HTTP 보안 프로토콜을 통해 요청을 허용하며 이는 차례로 SSL(Secure Sockets Layer) 또는 TLS(Transport Layer Security) 프로토콜에 의존합니다. HTTP 인터페이스에 대한 요청의 모든 URL은 `https` 프로토콜 스펙으로 시작합니다.

이 문서의 예에서는 `curl` 명령을 사용하여 서비스 HTTP 인터페이스를 호출합니다. 자세한 정보는 [curl 예제 사용](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl)을 참조하십시오. `curl`을 사용하는 HTTP 요청의 기본 형식은 다음 컴포넌트를 포함합니다.

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

중괄호 내의 변수값은 다음 정보를 제공합니다.

-   `{http_method}`는 HTTP 요청 메소드를 지정합니다. 예: `POST`, `PUT`, `GET` 또는 `DELETE`. 요청 메소드는 `GET` 외에 `curl`에 대해 필수입니다.
-   `{token}`은 사용자의 서비스 인스턴스에 대한 액세스 토큰을 제공합니다. 서비스에 대해 안전한 요청을 작성하기 위해 액세스 토큰을 사용해야 합니다.
-   `{method}`는 호출 중인 서비스의 메소드입니다. 예를 들어, `synthesize` 메소드를 사용하여 서비스에 대한 HTTP 요청을 작성할 수 있습니다.

나머지 변수값은 앞에서 설명한 정보를 제공합니다. 많은 메소드가 더 긴 이름을 가지며 요청의 일부로 지정해야 하는 경로 매개변수를 포함합니다. 대부분의 예제에는 요청 헤더, 조회 매개변수 및 기타 값도 포함됩니다.

예제는 HTTP 인터페이스에 대한 호출의 URL로 `{url}/v1/{method}`를 표시합니다. `{url}`을 방금 설명한 값으로 바꾸십시오.
{: note}

## 인증된 WebSocket 요청 작성
{: #websocketRequest}

{{site.data.keyword.texttospeechshort}} 서비스는 음성 합성만 제공하는 [WebSocket 인터페이스](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket)를 제공합니다. 서비스는 WebSocket 보안 프로토콜을 통해 요청을 허용하며 이는 다시 SSL(Secure Sockets Layer) 또는 TLS(Transport Layer Security) 프로토콜에 의존합니다. WebSocket 인터페이스에 대한 요청의 모든 URL은 `wss` 프로토콜 스펙으로 시작합니다.

애플리케이션 코드에서만 WebSocket 인터페이스를 호출할 수 있습니다. 명령행에서는 WebSocket 인터페이스를 호출할 수 없습니다. 다음 엔드포인트에서 서비스에 대한 WebSocket 연결을 설정할 수 있습니다.

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

변수값은 앞에서 설명한 정보를 제공합니다. 메소드의 `access_token` 조회 매개변수를 통해 액세스 토큰을 전달합니다.

예제는 WebSocket 인터페이스에 대한 호출의 URL로 `{ws_url}/v1/synthesize`를 표시합니다. `{ws_url}`을 방금 설명한 값으로 바꾸십시오.
{: note}

## SSL 검증 사용 안함
{: #SSLverification}

모든 Watson 서비스는 보안 연결 및 클라이언트와 서버 간의 통신에 SSL 또는 TLS를 사용합니다. 연결은 인증, 무결성 및 기밀성을 보장하기 위해 로컬 인증서 저장소에 대해 검증됩니다.

{{site.data.keyword.icp4dfull_notm}}에서 자체 서명된 인증서를 설치합니다. 인증서는 기본적으로 확인할 수 없습니다. 다음 중 하나를 사용하여 서비스 인스턴스에 연결할 수 있습니다.

-   자체 서명된 인증서를 사용자의 에이전트에 대한 신뢰 저장소에 추가하십시오.

    예를 들어, `curl`을 사용하여 보안 요청을 작성하려면 인증서를 `curl`에 대한 신뢰 저장소에 추가하십시오. 브라우저에서 보안 요청을 작성하려면 인증서를 브라우저에 대한 신뢰 저장소에 추가하십시오.
-   SSL 검증을 사용하지 않도록 설정하십시오.

    SSL 검증을 사용하지 않도록 설정하면 연결 및 데이터의 보안이 위협받습니다. 따라서 이 설정을 사용하지 않도록 강력히 권장합니다. 절대적으로 필요한 경우에만 SSL을 사용하지 않도록 설정하고 가능한 한 신속하게 SSL을 사용하도록 설정하십시오.
    {: important}

    -   `curl` 요청에 대해 SSL 검증을 사용하지 않도록 설정하려면 요청과 함께 `--insecure`(`-k`) 옵션을 사용하십시오. 이 옵션은 명령에 도구의 SSL 인증서 검증을 우회하도록 지시합니다.
    -   WebSocket 요청에 대해 SSL 검증을 사용하지 않도록 설정하려면 클라이언트 라이브러리에 대한 적절한 방법을 사용하거나 {{site.data.keyword.ibmwatson}} {{site.data.keyword.texttospeechshort}} SDK 중 하나를 사용하십시오.

서비스에 대한 호출에 SSL 검증을 사용하지 않도록 설정하는 방법에 대한 자세한 정보는 [API 참조](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}에서 *SSL 검증 사용 안함*을 참조하십시오. 정보에는 `curl` 및 모든 SDK에 대한 예제가 포함되어 있습니다.
