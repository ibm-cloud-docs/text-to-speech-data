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

# Sobre
{: #about}

O {{site.data.keyword.texttospeechdatafull}} para o {{site.data.keyword.icp4dfull}} fornece recursos de síntese de discurso para os seus aplicativos converterem texto escrito em discurso de sonoridade natural. O serviço flui os resultados de volta para o cliente com um atraso mínimo. O serviço oferece as interfaces [HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) e [WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).

Para obter informações sobre como instalar e configurar o {{site.data.keyword.texttospeechshort}} para o{{site.data.keyword.icp4dfull_notm}}, consulte[Instalando o serviço](/docs/services/text-to-speech-data?topic=text-to-speech-data-install).

O {{site.data.keyword.texttospeechdatafull}} para o {{site.data.keyword.icp4dfull}} é baseado no serviço do {{site.data.keyword.texttospeechfull}} no {{site.data.keyword.cloud_notm}} público. Para obter mais informações sobre o serviço público, consulte [Sobre o {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.
{: note}

## Recursos

O serviço {{site.data.keyword.texttospeechshort}} oferece os recursos a seguir:

-   **Formatos de áudio** - Produz áudio em Ogg ou WebM com o codec Opus ou Vorbis, WAV, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw ou formato básico. Para obter mais informações, consulte [Formatos de áudio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats).
-   **Vozes** - Sincroniza o texto para áudio em diversos idiomas, vozes e dialetos. Para obter mais informações, consulte [Idiomas e vozes](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).
-   **SSML** - Aceita texto sem formatação ou texto marcado com o Speech Synthesis Markup Language (SSML) baseado em XML. Para obter mais informações, consulte [Usando o SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml).
-   **Sincronizações de palavra** - Com a interface WebSocket, suporta o elemento `<mark>` do SSML e as informações opcionais de sincronização de palavra para todas as sequências do texto de entrada. As informações de sincronização sincronizam o texto de entrada e o áudio resultante. Para obter mais informações, consulte [Obtendo sincronizações de palavra](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing).
-   **Customização**-Fornece uma interface de customização que pode ser usada para especificar como o serviço pronuncia palavras incomuns que ocorrem em sua entrada. É possível definir pronúncias com o Alfabeto Fonético Internacional (IPA) ou com o {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). Para obter mais informações, consulte [Entendendo a customização](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).

## Suporte ao idioma
{: #languages-index}

O serviço suporta vozes nos seguintes idiomas: português do Brasil, inglês (dialetos britânico e americano), francês, alemão, italiano, japonês e espanhol (dialetos castelhano, da América Latina e da América do Norte).

O serviço oferece pelo menos uma voz feminina para cada idioma. Para alguns idiomas, o serviço oferece diversas vozes, incluindo vozes masculinas e femininas. Cada voz usa a cadência e a entonação apropriadas para seu dialeto.

Para obter mais informações sobre as vozes disponíveis para cada idioma, consulte [Idiomas e vozes](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).

Uma voz japonesa está pendente e estará disponível em breve.
{: note}

## Casos de uso
{: #usecases}

O serviço é apropriado para aplicativos orientados por voz e sem tela, nos quais o áudio é o método preferencial de saída:

-   Interfaces para pessoas com deficiência, como ferramentas de assistência para deficientes visuais
-   Leitura em voz alta de mensagens de texto e e-mails para motoristas
-   Narração de roteiros de vídeo e dublagem de vídeo
-   Ferramentas educacionais baseadas em leitura
-   Soluções de automação residencial

## Experimente o serviço

Para obter exemplos do serviço {{site.data.keyword.texttospeechshort}} em ação, consulte

-   Uma [demo rápida](https://text-to-speech-demo.ng.bluemix.net/){: external} do serviço {{site.data.keyword.texttospeechshort}} que aceita texto e gera discursos com vozes diferentes. Ela oferece a expressividade e a transformação, quando suportadas.
-   Aplicativos em [Kits do iniciador](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} do {{site.data.keyword.ibmwatson}} que demonstram o serviço {{site.data.keyword.texttospeechshort}}.
