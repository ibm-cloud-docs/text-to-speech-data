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

# Produktinformation
{: #about}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} stellt Sprachsynthesefunktionen für Ihre Anwendungen zur Verfügung, um geschriebenen Text in gut verständliche Sprache zu konvertieren. Der Service überträgt die Ergebnisse mit minimaler Verzögerung zurück an den Client. Er bietet Schnittstellen sowohl für [HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) als auch für [WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).

Informationen zur Installation und Konfiguration von {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} finden Sie in [Service installieren](/docs/services/text-to-speech-data?topic=text-to-speech-data-install).

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} basiert auf dem {{site.data.keyword.texttospeechfull}}-Service in der öffentlichen {{site.data.keyword.cloud_notm}}. Weitere Informationen zum öffentlichen Service finden Sie in der [Produktinformation zu {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.
{: note}

## Features und Funktionen

Der {{site.data.keyword.texttospeechshort}}-Service bietet die folgenden Features und Funktionen:

-   **Audioformate** - Erzeugt Sprachausgabe im Ogg- oder WebM-Format mit Opus- oder Vorbis-Codec, im WAV-Format, FLAC-Format, MP3-Format (MPEG), l16-Format (PCM), Mu-Law-Format oder im Basisformat. Weitere Informationen finden Sie unter [Audioformate](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats).
-   **Stimmen** - Erstellt aus Text synthetisch Sprachausgabe in verschiedenen Sprachen, Stimmen und Dialekten. Weitere Informationen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).
-   **SSML** - Akzeptiert einfachen Text oder Text mit der XML-basierten Markup-Sprache 'Speech Synthesis Markup Language' (SSML). Weitere Informationen finden Sie im Abschnitt [SSML verwenden](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml).
-   **Worttakt** - Unterstützt bei der WebSocket-Schnittstelle das SSML-Element `<mark>` und optionale Worttaktinformationen für alle Zeichenfolgen des Eingabetextes. Die Taktinformationen synchronisieren den Eingabetext und die resultierende Sprachausgabe. Weitere Informationen finden Sie unter [Worttakt abrufen](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing).
-   **Anpassung** - Bietet eine Anpassungsschnittstelle, mit der Sie angeben können, wie der Service ungewöhnliche Wörter aussprechen soll, die in der Eingabe enthalten sind. Zum Definieren der Aussprachevarianten können Sie IPA (International Phonetic Alphabet, internationales phonetisches Alphabet) oder {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) verwenden. Weitere Informationen enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).

## Sprachunterstützung
{: #languages-index}

Der Service unterstützt Stimmen in den folgenden Sprachen: brasilianisches Portugiesisch, Englisch (britischer und amerikanischer Dialekt), Französisch, Deutsch, Italienisch, Japanisch und Spanisch (kastilischer, lateinamerikanischer und nordamerikanischer Dialekt).

Der Service bietet für jede Sprache mindestens eine Frauenstimme an. Für einige Sprachen bietet der Service mehrere Stimmen an, darunter sowohl Männer- als auch Frauenstimmen. Jede Stimme verwendet den geeigneten Tonfall und die passende Satzmelodie für ihren Dialekt.

Weitere Informationen zu den Stimmen, die für jede Sprache verfügbar sind, finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).

Eine japanische Stimme steht künftig bereit und ist in Kürze verfügbar.
{: note}

## Anwendungsfälle
{: #usecases}

Der Service ist für sprachgesteuerte und anzeigenlose Anwendungen geeignet, bei denen vorzugsweise Audioausgabe verwendet wird:

-   Schnittstellen für Personen mit körperlichen Beeinträchtigungen wie beispielsweise Assistenztools für Sehbehinderte
-   Funktionen zum Vorlesen von Text und E-Mail-Nachrichten für Autofahrer
-   Drehbuchkommentare und Off-Kommentare für Videos
-   Lesebasierte Lernmittel
-   Lösungen für die Haushaltsautomation

## Service ausprobieren

Beispiele für die Ausführung des {{site.data.keyword.texttospeechshort}}-Service bieten die folgenden Quellen:

-   Eine [Kurzdemo](https://text-to-speech-demo.ng.bluemix.net/){: external} des {{site.data.keyword.texttospeechshort}}-Service, der Text als Eingabe verwendet und Sprachausgabe in verschiedenen Stimmen generiert. Bei entsprechender Unterstützung bietet der Service Expressivität und Stimmenumwandlung.
-   Anwendungen in {{site.data.keyword.ibmwatson}}[Starter Kits](http://www.ibm.com/watson/developercloud/starter-kits.html){: external}, die den {{site.data.keyword.texttospeechshort}}-Service vorführen.
