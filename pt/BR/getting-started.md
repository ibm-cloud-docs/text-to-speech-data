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

# Tutorial de introdução
{: #gettingStarted}

O {{site.data.keyword.texttospeechdatafull}} para o {{site.data.keyword.icp4dfull}} converte texto escrito em discurso de sonoridade natural para fornecer recursos de síntese de discurso para aplicativos. Esse tutorial baseado em curl pode ajudá-lo a começar rapidamente a usar o serviço. Os exemplos mostram como chamar os métodos `POST` e `GET /v1/synthesize` do serviço para solicitar um fluxo de áudio.
{: shortdesc}

## Antes de começar
{: #before-you-begin}

Para usar o {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}}, deve-se primeiro concluir as etapas a seguir:

1.  Provisione uma instância do {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}}. Para obter mais informações sobre fornecimento, consulte [Instalando o serviço](/docs/services/text-to-speech-data?topic=text-to-speech-data-install).
1.  No menu do Web client do {{site.data.keyword.icp4dfull_notm}}, escolha **Minhas instâncias**.
1.  Clique na instância do {{site.data.keyword.texttospeechshort}} para abrir a página de visão geral. Copie os valores de credencial `{token}` e `{URL}`.

### Usando os exemplos de curl
{: #getting-started-curl}

Esse tutorial usa o comando `curl` para chamar métodos da interface HTTP do serviço. Certifique-se de ter o comando `curl` instalado em seu sistema.

1.  Para testar se o `curl` está instalado, execute o comando a seguir na linha de comandos. Se a saída listar a versão do `curl` que suporta Secure Sockets Layer (SSL), tudo estará configurado para o tutorial.

    ```bash
    curl -V
    ```
    {: pre}

1.  Se necessário, instale a versão do `curl` com SSL ativado para seu sistema operacional em
[curl.haxx.se](https://curl.haxx.se/){: external}.

Omita os colchetes dos exemplos. Eles indicam valores de variáveis.
{: tip}

## Etapa 1: sintetizar textos em inglês americano
{: #synthesizeEnglish}

Os comandos a seguir usam o método `POST /v1/synthesize` para sintetizar a entrada em inglês americano para arquivos de áudio em dois formatos diferentes. Ambas as solicitações usam a voz padrão em inglês americano, `en-US_MichaelVoice`.

1.  Emita o comando a seguir para sintetizar a sequência "hello world" e produzir um arquivo WAV denominado `hello_world.wav`.
    -   Substitua `{token}` pelo token de acesso para a sua instância de serviço.
    -   Substitua `{url}` pela URL para sua instância de serviço.

    *Usuários do Windows,* substituam a barra invertida (``\`) no final de cada linha por um acento circunflexo (``^`). Certifiquem-se de que não haja espaços à direita.
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

1.  Emita o comando a seguir para sintetizar o mesmo texto, mas produzir um arquivo Ogg (o formato padrão) denominado `hello_world.ogg`.
    -   Substitua `{token}` pelo token de acesso para a sua instância de serviço.
    -   Substitua `{url}` pela URL para sua instância de serviço.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"
    ```
    {: pre}

É possível usar um navegador ou outras ferramentas para reproduzir os arquivos de áudio que são produzidos pelos exemplos. Para obter mais informações, consulte [Reproduzindo um arquivo de áudio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats#formatsPlay).
{: note}

## Etapa 2: sintetizar textos em espanhol
{: #synthesizeSpanish}

O comando a seguir usa o método `GET /v1/synthesize` para sintetizar uma entrada em espanhol para um arquivo de áudio.

1.  Emita o comando a seguir para sintetizar a sequência "hola mundo" e produzir um arquivo WAV denominado `hola_mundo.wav`. O texto de entrada é codificado com URL. O método inclui os parâmetros de consulta `accept` para especificar o formato de áudio e a `voice` para especificar uma voz espanhola, `es-ES_EnriqueV3Voice`.
    -   Substitua `{token}` pelo token de acesso para a sua instância de serviço.
    -   Substitua `{url}` pela URL para sua instância de serviço.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

## Próximas etapas

-   Saiba mais sobre a interface HTTP do serviço em [A interface HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP).
-   Saiba mais sobre a interface WebSocket do serviço em [A interface WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).
-   Localize informações detalhadas sobre todos os métodos das interfaces do serviço na [Referência de API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
