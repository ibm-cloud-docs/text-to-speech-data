---

copyright:
  years: 2019
lastupdated: "2019-07-08"

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

# 서비스의 기반이 된 과학
{: #science}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}는 입력 텍스트에서 인간 음성을 합성하기 위해 신경 음성 기술에 의존합니다. 신경 음성을 통해서는 매우 자연스럽게 들리고 부드러운 오디오 품질의 또렷하고 명확한 음성을 생성합니다.
{: shortdesc}

서비스에서는 먼저 원하는 컨텐츠를 판별하기 위해 입력 텍스트를 분석합니다. 그런 다음 의사결정 트리로 구성된 음향 모델을 사용하여 합성할 후보 단위를 생성합니다. 합성될 전화의 순서로 된 각 전화마다 모델은 두 전화 앞뒤의 컨텍스트에서 전화를 고려합니다. 그런 다음 적합성을 평가하는 음향 단위 세트가 생성됩니다. 이 단계를 통해 일부 컨텍스트 기준을 충족시키는 해당 단위로만 검색의 복잡도를 제한하고 기타 모든 항목은 삭제하여 검색의 복잡도가 감소됩니다.

그러면 서비스에서 세 개의 DNN(Deep Neural Network)을 사용하여 음성의 음향(스펙트럼) 기능을 예측하고 결과적으로 생성되는 오디오를 인코딩합니다.

-   운율 예측
-   음향 기능 예측
-   신경 보코더

합성 중에 DNN에서 음높이와 음소 기간(운율), 스펙트럼 구조 및 음성의 파형을 예측합니다. 예를 들어 운율 예측 모듈에서는 입력 텍스트에서 추출한 언어적 특성의 대상 값을 생성합니다. 이 특성에는 품사, 어휘의 강세, 단어 레벨 중요성 및 위치 특성(예: 문장에서 음절 또는 단어의 위치)과 같은 속성이 포함됩니다.

DNN은 오디오의 음향 특성을 예측하기 자연스러운 인간의 음성을 학습합니다. 이 모듈식 접근 방식을 사용하면 각 컴포넌트를 개별적으로 제어하면서 빠르고 쉽게 학습시킬 수 있는 이점이 있습니다. 기본 네트워크를 학습시키고 나면 브랜드화와 개인화를 위해 새로운 말하기 스타일 또는 음성에 맞게 조정할 수 있습니다.

서비스의 신경 음성 기술에 관한 자세한 정보는 다음을 참조하십시오.

-   블로그 게시물 [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   연구 문서 [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

문자-음성 변환 합성 주제는 기본적으로 복잡합니다. 서비스의 음성 기술의 기반이 되는 과학적 연구에 대한 자세한 정보는 [참고 문헌](/docs/services/text-to-speech-data?topic=text-to-speech-data-references)을 참조하십시오.
