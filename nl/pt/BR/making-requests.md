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

# Fazendo solicitações para o serviço
{: #making-requests}

Para fazer solicitações autenticadas para o {{site.data.keyword.texttospeechdatafull}} para o {{site.data.keyword.icp4dfull}}, você provisiona uma instância do serviço e obtém credenciais. Você usa uma URL diferente para as interfaces de HTTP e WebSocket do serviço. Se você usar um certificado autoassinado, será necessário desativar a verificação de SSL para solicitações para o serviço.
{: shortdesc}

## Provisionando uma instância e obtendo credenciais
{: #making-requests-provisioning}

Antes de usar o serviço do {{site.data.keyword.texttospeechshort}}, deve-se provisionar uma instância do serviço e obter as suas credenciais. Para obter mais informações, consulte [Antes de iniciar](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin). Na última etapa desse procedimento, você copia o `{token}` e `{URL}` para a sua instância de serviço:

-   O `{token}` fornece o seu token de acesso para autenticar para o serviço. É possível usar o token de acesso exibido no Web client do {{site.data.keyword.icp4dfull_notm}}. No entanto, em um ambiente de produção, use um token que você gera programaticamente para a sua instância de serviço. Para obter mais informações e para obter exemplos, consulte *Autenticação* na [Referência de API](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}.

    Você autentica para o serviço do {{site.data.keyword.texttospeechshort}} transmitindo o seu token de acesso com cada solicitação. O {{site.data.keyword.texttospeechshort}} para o {{site.data.keyword.icp4dfull_notm}} é uma solução de nuvem de vários locatários. As suas credenciais fornecem acesso somente aos seus dados e os seus dados são isolados de outros usuários.
-   A `{URL}` fornece o terminal base que você usa para chamar métodos do serviço.

A URL contém os componentes a seguir:

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

Os valores da variável em `{}` (chaves) fornecem as informações a seguir:

-   `{icp4d_cluster_host}` é o nome ou o endereço IP do host no qual o seu cluster do {{site.data.keyword.icp4dfull_notm}} está implementado.
-   `{:port}` é o número da porta na qual o serviço atende a pedidos no host especificado. Deve-se preceder o número da porta com `:` (dois pontos).
-   `{release}` é o nome da liberação que foi especificado quando o gráfico do Helm foi instalado.
-   `{instance_id}` é o identificador de sua instância de serviço.

As chaves indicam sequências variáveis que deve-se substituir por valores literais. Não inclua as chaves em chamadas reais para o serviço.
{: note}

## Fazendo uma solicitação de HTTP autenticada
{: #httpRequest}

O serviço do {{site.data.keyword.texttospeechshort}} oferece uma [interface de HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) que fornece acesso a todas as funcionalidades do serviço, incluindo as interfaces de customização. A interface de HTTP aceita pedidos sobre o protocolo HTTP Seguro, que, por sua vez, depende do protocolo Secure Sockets Layer (SSL) (ou Transport Layer Security (TLS)). Todas as URLs para solicitações para a interface de HTTP começam com a especificação de protocolo `https`.

Os exemplos nesta documentação usam o comando `curl` para chamar a interface de HTTP do serviço. Para obter mais informações, consulte [Usando os exemplos de curl](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl). O formato básico de uma solicitação de HTTP com `curl` inclui os componentes a seguir:

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

Os valores da variável entre chaves fornecem as seguintes informações:

-   `{http_method}` especifica o método de solicitação de HTTP para o exemplo: `POST`, `PUT`, `GET` ou `DELETE`. O método de solicitação é necessário com `curl` para qualquer coisa diferente de `GET`.
-   `{token}` fornece o token de acesso para a sua instância de serviço. Deve-se usar o token de acesso para fazer uma solicitação segura para o serviço.
-   `{method}` é o método do serviço que você está chamando. Por exemplo, você usa o método `synthesize` para fazer uma solicitação de HTTP para o serviço.

Os valores da variável restantes fornecem as informações que foram descritas anteriormente. Muitos métodos têm nomes mais longos e incluem parâmetros de caminho que deve-se especificar como parte da solicitação. A maioria dos exemplos também inclui cabeçalhos de solicitação, parâmetros de consulta e outros valores.

Os exemplos mostram a URL para chamadas para a interface de HTTP como `{url}/v1/{method}`. Substitua `{url}` pelos valores que acabaram de ser descritos.
{: note}

## Fazendo uma solicitação de WebSocket autenticada
{: #websocketRequest}

O serviço do {{site.data.keyword.texttospeechshort}} oferece uma [interface do WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) que fornece apenas a síntese de discurso. O serviço aceita solicitações por meio do protocolo WebSocket Secure, que novamente depende do protocolo Secure Sockets Layer (SSL) (ou Transport Layer Security (TLS)). Todas as URLs para pedidos para a interface do WebSocket iniciam com a especificação de protocolo `wss`.

É possível chamar a interface do WebSocket somente por meio do código do aplicativo. Não é possível chamar a interface do WebSocket por meio da linha de comandos. Você estabelece uma conexão do WebSocket com o serviço no terminal a seguir.

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

Os valores da variável fornecem as informações que foram descritas anteriormente. Você transmite o seu token de acesso por meio do parâmetro de consulta `access_token` do método.

Os exemplos mostram a URL para chamadas para a interface do WebSocket como `{ws_url}/v1/synthesize`. Substitua `{ws_url}` pelos valores que acabaram de ser descritos.
{: note}

## Desativando a verificação de SSL
{: #SSLverification}

Todos os serviços do Watson usam SSL (ou TLS) para conexões seguras e comunicações entre o cliente e o servidor. A conexão é verificada com relação ao armazenamento de certificados local para garantir autenticação, integridade e confidencialidade.

O {{site.data.keyword.icp4dfull_notm}} instala um certificado autoassinado. Esse certificado não pode ser verificado com êxito por padrão. É possível executar uma das ações a seguir para se conectar com êxito a uma instância de serviço:

-   Inclua o certificado autoassinado no armazenamento confiável para o seu agente do usuário.

    Por exemplo, para fazer solicitações seguras com `curl`, inclua o certificado no armazenamento confiável para `curl`. Para fazer solicitações seguras por meio de seu navegador, inclua o certificado no armazenamento confiável para o navegador.
-   Desative a verificação de SSL.

    Desativar a verificação SSL compromete a segurança da conexão e dos dados. É altamente desaconselhável. Desative o SSL apenas se for absolutamente necessário e tome as providências para ativar o SSL assim que possível.
    {: important}

    -   Para desativar a verificação de SSL para uma solicitação `curl`, use a opção `--insecure` (`-k`) com a solicitação. Esta opção direciona o comando para efetuar bypass da verificação da ferramenta de certificados SSL.
    -   Para desativar a verificação de SSL para uma solicitação do WebSocket, use a abordagem apropriada para a sua biblioteca do cliente ou use um dos SDKs do {{site.data.keyword.ibmwatson}} {{site.data.keyword.texttospeechshort}}.

Para obter mais informações sobre a desativação da verificação de SSL para chamadas para o serviço, consulte *Desativando a verificação de SSL* na [Referência de API](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}. As informações incluem exemplos para `curl` e para todos os SDKs.
