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

# A ciência por trás do serviço
{: #science}

O {{site.data.keyword.texttospeechdatafull}} para o {{site.data.keyword.icp4dfull}} depende da tecnologia de voz neural para sintetizar o discurso de qualidade humana por meio do texto de entrada. As vozes neurais produzem um discurso nítido e limpo, com uma qualidade de áudio muito natural e suave.
{: shortdesc}

Primeiro, o serviço analisa o texto de entrada para determinar o conteúdo desejado. Ele usa um modelo acústico que consiste em uma árvore de decisão para gerar as unidades candidatas para síntese. Para cada fonema em uma sequência de fonemas a serem sintetizados, o modelo o considera no contexto do anterior e do seguinte. Em seguida, ele produz um conjunto de unidades acústicas que são avaliadas com relação à adequação. Essa etapa reduz a complexidade da procura restringindo-a somente àquelas unidades que atendem a alguns critérios contextuais e descartando todas as outras.

Em seguida, o serviço usa três Redes Neurais Profundas (DNNs) para prever os recursos acústicos (espectrais) do discurso e codificar o áudio resultante:

-   Predição de prosódia
-   Predição do recurso acústico
-   Vocoder neural

Durante a síntese, as DNNs preveem a duração do tom e do fonema (prosódia), a estrutura espectral e a forma de onda do discurso. Por exemplo, o módulo de predição de prosódia gera valores de destino para os recursos linguísticos que são extraídos do texto de entrada. Os recursos incluem atributos como parte do discurso, acento lexical, proeminência de nível de palavra e recursos posicionais, como a posição da sílaba ou da palavra na sentença.

As DNNs são treinadas em discursos humanos naturais para prever os recursos acústicos do áudio. Essa abordagem modular tem a vantagem de permitir o treinamento de uma maneira rápida e fácil e o controle independente de cada componente. Depois que as redes de base são treinadas, podem ser adaptadas para novos estilos de fala ou vozes para fins de branding e personalização.

Para obter mais informações sobre a tecnologia de voz neural do serviço, consulte

-   A postagem do blog [IBM
Watson Text to Speech: vozes neurais com disponibilidade geral](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   O documento de pesquisa [Text to Speech de alta qualidade, leve e adaptável usando o LPCNet](https://arxiv.org/abs/1905.00590){: external}

O tópico de sintetização de texto para voz é inerentemente complexo. Para obter mais informações sobre a pesquisa científica por trás da tecnologia de fala do serviço, consulte os documentos listados em [Referências de pesquisa](/docs/services/text-to-speech-data?topic=text-to-speech-data-references).
