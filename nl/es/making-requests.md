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

# Cómo realizar solicitudes al servicio
{: #making-requests}

Para efectuar solicitudes autenticadas a {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}, suministre una instancia del servicio y consiga las credenciales. Utilice un URL distinto para las interfaces HTTP y WebSocket del servicio. Si utiliza un certificado firmado automáticamente, tendrá que inhabilitar la verificación de SSL de las solicitudes al servicio.
{: shortdesc}

## Suministro de una instancia y obtención de credenciales
{: #making-requests-provisioning}

Antes de utilizar el servicio {{site.data.keyword.texttospeechshort}}, debe suministrar una instancia del servicio y obtener sus credenciales. Para obtener más información, consulte la sección [Antes de empezar](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin). En el último paso de este procedimiento, copie la `{señal}` y el `{URL}` de su instancia de servicio:

-   La `{señal}` proporciona la señal de acceso para la autenticación al servicio. Puede utilizar la señal de acceso visualizada en el cliente web de {{site.data.keyword.icp4dfull_notm}}. Sin embargo, en un entorno de producción, utilice una señal que genere programáticamente para su instancia de servicio. Para obtener más información así como ejemplos, consulte *Autenticación* en [Consulte de API](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}.

    Se autentica al servicio {{site.data.keyword.texttospeechshort}} pasando la señal de acceso con cada solicitud. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} es una solución en la nube de multiarrendatario. Sus credenciales proporcionan acceso solamente a los datos y los datos están aislados de otros usuarios.
-   El `{URL}` proporciona el punto final base que utilizará para llamar a los métodos de servicio.

El URL contiene los siguientes componentes:

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

Los valores de variable entre `{}` (llaves) proporcionan la información siguiente:

-   `{icp4d_cluster_host}` es el nombre o la dirección IP del host donde se ha desplegado el clúster de {{site.data.keyword.icp4dfull_notm}}.
-   `{:port}`es el número de puerto donde el servicio permanece a la escucha de solicitudes en el host especificado. Antes del número de puerto se debe escribir el carácter `:` (dos puntos).
-   `{release}` es el nombre del release que se ha especificado cuando se ha instalado la gráfica de Helm.
-   `{ID_instance}` es el identificador de la instancia de servicio.

Las llaves indican series de variables que se deben sustituir con valores literales. No incluya las llaves en las llamadas reales al servicio.
{: note}

## Cómo realizar una solicitud HTTP autenticada
{: #httpRequest}

El servicio {{site.data.keyword.texttospeechshort}} ofrece una [interfaz HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) que proporciona acceso a todas las funciones de servicio, incluidas las interfaces de personalización. La interfaz HTTP acepta solicitudes a través del protocolo HTTP seguro que, a su vez, se basa en el protocolo Secure Sockets Layer (SSL) (o Transport Layer Security (TLS)). Todos los URL para las solicitudes a la interfaz HTTP empiezan por la especificación de protocolo `https`.

Los ejemplos de esta documentación utilizan el mandato `curl` para llamar la interfaz HTTP de servicio. Para obtener más información, consulte [Utilización de los ejemplos de curl](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl). El formato básico de una solicitud HTTP con `curl` incluye los componentes siguientes:

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

Los valores de variables entre llaves proporcionan la información siguiente:

-   `{método_http}` especifica el método de solicitud HTTP para el ejemplo: `POST`, `PUT`, `GET` o `DELETE`. El método de solicitud es necesario con `curl` para cualquier otro valor que no sea `GET`.
-   `{señal}` proporciona la señal de acceso para su instancia de servicio. Debe utilizar la señal de acceso para realizar una solicitud segura al servicio.
-   `{método}` es el método del servicio que está llamando. Por ejemplo, utilice el método `synthesize` para efectuar una solicitud HTTP al servicio.

El resto de valores de variables proporcionan la información que se ha descrito anteriormente. Muchos métodos tienen nombres largos e incluyen parámetros de vía de acceso que se deben especificar como parte de la solicitud. La mayoría de los ejemplos también incluyen cabeceras, parámetros de consulta y otros valores.

Los ejemplos muestran el URL para las llamadas a la interfaz HTTP como `{url}/v1/{método}`. Sustituya `{url}` por los valores que se acaban de describir.
{: note}

## Cómo realizar una solicitud WebSocket autenticada
{: #websocketRequest}

El servicio {{site.data.keyword.texttospeechshort}} ofrece una [interfaz WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) que sólo proporciona síntesis de voz. El servicio acepta solicitudes a través del protocolo WebSocket Secure que, a su vez, se basa en el protocolo Secure Sockets Layer (SSL) (o Transport Layer Security (TLS)). Todos los URL para las solicitudes a la interfaz WebSocket empiezan por la especificación de protocolo `wss`.

Puede llamar a la interfaz WebSocket sólo desde el código de la aplicación. No puede llamar a la interfaz WebSocket desde la línea de mandatos. Puede establecer una conexión WebSocket al servicio en el siguiente punto final.

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

Los valores de variables proporcionan la información que se ha descrito anteriormente. Se pasa la señal de acceso a través del parámetro de consulta `access_token` del método.

Los ejemplos muestran el URL para las llamadas a la interfaz WebSocket como `{ws_url}/v1/synthesize`. Sustituya `{ws_url}` por los valores que se acaban de describir.
{: note}

## Inhabilitación de la verificación de SSL
{: #SSLverification}

Todos los servicios Watson utilizan SSL (o TLS) para conexiones y comunicaciones seguras entre el cliente y el servidor. La conexión se verifica en el almacén de certificados local para garantizar la autenticación, la integridad y la confidencialidad.

{{site.data.keyword.icp4dfull_notm}} instala un certificado firmado automáticamente. De forma predeterminada, este certificado no se puede verificar satisfactoriamente. Puede realizar una de las acciones siguientes para conectarse de forma satisfactoria a una interfaz de servicio:

-   Añadir el certificado firmado automáticamente en el almacén de confianza para su agente de usuario.

    Por ejemplo, para realizar solicitudes seguras con `curl` y el certificado al almacén de confianza para `curl`. Si desea realizar solicitudes seguras desde el navegador, añada el certificado en el almacén de confianza del navegador.
-   Inhabilitar la verificación de SSL.

    La inhabilitación de la verificación de SSL compromete la seguridad de la conexión y los datos. No se recomienda en absoluto. Inhabilite SSL solamente si es absolutamente necesario y vuelva a los pasos para habilitar SSL tan pronto como le sea posible.
    {: important}

    -   Para inhabilitar la verificación de SSL para una solicitud `curl`, utilice la opción `--insecure` (`-k`) con la solicitud. Esta opción dirige el mandato a ignorar la verificación de herramienta de certificados SSL.
    -   Para inhabilitar la verificación de SSL para una solicitud WebSocket, utilice el enfoque adecuado para la biblioteca de cliente o utilice uno de los SDK de {{site.data.keyword.ibmwatson}} {{site.data.keyword.texttospeechshort}}.

Para obtener más información sobre cómo inhabilitar la verificación de SSL para las llamadas al servicio, consulte
*Inhabilitación de la verificación de SSL* en [Consulta API](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}. La información incluye ejemplos de `curl` y de todos los SDK.
