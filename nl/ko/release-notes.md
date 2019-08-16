---

copyright:
  years: 2019
lastupdated: "2019-06-24"

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

# 릴리스 정보
{: #release-notes}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}의 다음 버전이 사용 가능합니다. 정보에는 제품의 각 버전에 대한 새 기능 및 변경사항과 알려진 제한사항이 포함됩니다.
{: shortdesc}

## 알려진 제한사항
{: #limitations}

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}에는 다음과 같은 알려진 제한사항이 있습니다.

-   신경 일본어 음성 `ja-JP_EmiV3Voice`는 아직 사용 가능하지 않습니다. 지원이 보류 중이며 곧 사용 가능하게 됩니다.

### 버전 1.0.0(2019년 6월)
{: #v100}

서비스의 초기 릴리스입니다. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}는 퍼블릭 {{site.data.keyword.cloud_notm}}의 {{site.data.keyword.texttospeechfull}} 서비스를 기반으로 합니다. 퍼블릭 서비스에 대한 자세한 정보는 [{{site.data.keyword.texttospeechshort}} 정보](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}를 참조하십시오.

{{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}는 퍼블릭 {{site.data.keyword.texttospeechshort}} 서비스와 다음 측면에서 다릅니다. 이미 퍼블릭 {{site.data.keyword.cloud_notm}}의 {{site.data.keyword.texttospeechshort}} 서비스에 익숙한 경우, 이 정보가 유용할 것입니다.

-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}에서는 인증을 위해 액세스 토큰이 필요합니다. 자세한 정보는 [서비스에 대한 요청 작성](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) 및 [API 참조](https://{DomainName}/apidocs/text-to-speech-data){: external}를 확인하십시오.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}에 대한 엔드포인트는 사용자의 {{site.data.keyword.icp4dfull_notm}} 클러스터에 고유합니다. 자세한 정보는 [서비스에 대한 요청 작성](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) 및 [API 참조](https://{DomainName}/apidocs/text-to-speech-data){: external}를 확인하십시오.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}에서는 신경 음성만 지원합니다. 표준(연결) 음성은 지원하지 않습니다. 신경 음성은 SSML `<express-as>` 및 `<voice-transformation>` 요소를 지원하지 않습니다.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}는 요청 로깅을 수행하지 않습니다. `X-Watson-Learning-Opt-Out` 요청 헤더를 사용할 필요가 없습니다.
-   {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}는 Watson 토큰을 지원하지 않습니다. 서비스에 인증하기 위해 `X-Watson-Authorization-Token` 요청 헤더를 사용할 수 없습니다.
