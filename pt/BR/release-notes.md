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

# Nota sobre a Liberação
{: #release-notes}

As versões a seguir do {{site.data.keyword.texttospeechdatafull}} para o {{site.data.keyword.icp4dfull}} estão disponíveis. As informações incluem novos recursos e mudanças para cada versão do produto e quaisquer limitações conhecidas.
{: shortdesc}

## Limitações conhecidas
{: #limitations}

O {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}} tem a limitação conhecida a seguir:

-   A voz neural japonesa `ja-JP_EmiV3Voice` ainda não está disponível. O suporte está pendente e estará disponível em breve.

### Versão 1.0.0 (Junho de 2019)
{: #v100}

A liberação inicial do serviço. O {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}} é baseado no serviço do {{site.data.keyword.texttospeechfull}} no {{site.data.keyword.cloud_notm}} público. Para obter mais informações sobre o serviço público, consulte [Sobre o {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.

O {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}} difere do serviço do {{site.data.keyword.texttospeechshort}} público das maneiras a seguir. Você poderá achar essas informações úteis se já estiver familiarizado com o serviço do {{site.data.keyword.texttospeechshort}} no {{site.data.keyword.cloud_notm}} público.

-   O {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}} usa tokens de acesso para autenticação. Para obter mais informações, consulte [Fazendo solicitações para o serviço](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) e a [Referência de API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   Os terminais para o {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}} são específicos para o seu cluster do {{site.data.keyword.icp4dfull_notm}}. Para obter mais informações, consulte [Fazendo solicitações para o serviço](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests) e a [Referência de API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
-   O {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}} suporta apenas vozes neurais. Ele não suporta vozes padrão (concatenativas). As vozes neurais não suportam os elementos `<express-as>` e `<voice-transformation>` de SSML.
-   O {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}} não executa nenhuma criação de log de solicitação. Você não precisa usar o cabeçalho de solicitação `X-Watson-Learning-Opt-Out`.
-   O {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}} não suporta tokens do Watson. Não é possível usar o cabeçalho da solicitação `X-Watson-Authorization-Token` para autenticar-se com o serviço.
