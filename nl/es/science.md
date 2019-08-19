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

# La ciencia detrás del servicio
{: #science}

{{site.data.keyword.texttospeechdatafull}} para {{site.data.keyword.icp4dfull}} se basa en la tecnología de voz neuronal para sintetizar el habla de calidad humana a partir del texto de entrada. Las voces neuronales generan habla que es nítida y clara, con una calidad de sonido muy natural y suave.
{: shortdesc}

El servicio analiza primero el texto de entrada para determinar el contenido deseado. Utiliza un modelo acústico que consta de un árbol de decisiones para generar unidades candidatas para la síntesis. Para cada uno de los teléfonos de una secuencia de teléfonos a sintetizar, el modelo considera el teléfono en el contexto de los dos teléfonos anteriores y posteriores. A continuación, produce un conjunto de unidades acústicas de las que se evalúa su adecuación. Este paso reduce la complejidad de la búsqueda restringiéndola a sólo aquellas unidades que cumplen algunos criterios contextuales y descartando todas las demás.

El servicio utiliza a continuación las redes neuronales profundas (DNN - Deep Neural Networks) para predecir las características acústicas (espectrales) del habla y codificar el audio que se genera:

-   Predicción de prosodia
-   Predicción de característica acústica
-   Codificador de voz neuronal

Durante la síntesis, las DNN predicen el tono y la duración del fonema (prosodia), la estructural espectral y la forma de onda del habla. Por ejemplo, el módulo de predicción de la prosodia genera valores de destina para las funciones lingüísticas que se extraen del texto de entrada. Las funciones incluyen este tipo de atributos como parte de la categoría léxica, el acento léxico, la prominencia a nivel de palabra y las características de posición como, por ejemplo, la posición de la sílaba o la palabra en la frase.

Las DNN se basan en el habla humana natural para predecir características acústicas del audio. Este enfoque modular tiene la ventaja de permitir una formación rápida y fácil, así como un control independiente de cada componente. Una vez formadas las redes básicas, se pueden adaptar a los nuevos estilos de habla y a las nuevas voces con fines de personalización o de imagen corporativa.

Para obtener más información sobre la tecnología de voz neuronal del servicio, consulte

-   La publicación de blog [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   El documento de investigación [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

El tema de sintetizar el texto a habla es inherentemente complejo. Para obtener más información sobre la investigación científica que hay detrás de la tecnología de habla del servicio, consulte [Referencias de investigación](/docs/services/text-to-speech-data?topic=text-to-speech-data-references).
