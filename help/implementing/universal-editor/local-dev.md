---
title: Kör din egen universella redigeringstjänst
description: Lär dig hur du kan köra din egen Universal Editor-tjänst för lokal utveckling eller som en del av din egen infrastruktur.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 54d1cdec9b30c08f28d4c9b2fbd97446f3ff05b3
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---


# Kör din egen universella redigeringstjänst {#local-ue-service}

Lär dig hur du kan köra din egen Universal Editor-tjänst för lokal utveckling eller som en del av din egen infrastruktur.

## Ökning {#overview}

Universal Editor-tjänsten är den som binder Universal Editor och serverdelssystemet. Om du vill kunna utveckla lokalt för den universella redigeraren måste du köra en lokal kopia av den universella redigeringstjänsten. Detta beror på:

* Adobe officiella universell redigeringstjänst finns på en global värdserver och din lokala AEM måste vara exponerad för Internet.
* När du utvecklar med en lokal AEM SDK går det inte att komma åt Adobe universella redigeringstjänst från Internet.
* Om din AEM har IP-begränsningar och Adobe Universal Editor-tjänsten inte har ett definierat IP-intervall kan du själv vara värd för den.

## Användningsexempel {#use-cases}

Din egen kopia av Universal Editor-tjänsten är användbar om du vill:

* Utveckla lokalt på AEM för användning med den universella redigeraren.
* Kör din egen universella redigeringstjänst som en del av din egen infrastruktur, oberoende av Adobe universella redigeringstjänst.

Båda användningsfallen stöds. I det här dokumentet förklaras hur du kör AEM i HTTPS tillsammans med en lokal kopia av den universella redigeringstjänsten.

Om du vill köra din egen Universal Editor-tjänst som en del av din egen infrastruktur följer du samma steg som det lokala utvecklingsexemplet.

## Konfigurera AEM som ska köras på HTTPS {#aem-https}

I en yttre ram som skyddas med HTTPS går det inte att läsa in en osäker HTTP-ram. Tjänsten Universal Editor körs på HTTPS och därför måste AEM eller andra fjärrsidor också köras på HTTPS.

För att göra detta måste du konfigurera AEM för att köra HTTPS. I utvecklingssyfte kan du använda självsignerade certifikat.

[Se det här dokumentet](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html) om hur du konfigurerar AEM som körs på HTTPS, inklusive ett självsignerat certifikat som du kan använda.

## Installera Universal Editor-tjänsten {#install-ue-service}

Den universella redigeringstjänsten är inte en fullständig kopia av den universella redigeraren, utan bara en delmängd av dess funktioner för att säkerställa att samtal från den lokala AEM inte dirigeras över Internet, utan från en definierad slutpunkt som du kontrollerar.

[NodeJS version 20](https://nodejs.org/en/download/releases) krävs för att köra en lokal kopia av Universal Editor-tjänsten.

Tjänsten Universal Editor är tillgänglig via Software Distribution. Mer information om hur du får åtkomst till programdistributionsdokumentationen finns i [dokumentationen för programvarudistribution](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html).

Spara filen `universal-editor-service.cjs` från programvarudistribution till den lokala utvecklingsmiljön.

## Skapa ett certifikat som kör den universella redigeringstjänsten med HTTPS {#ue-https}

Tjänsten Universal Editor kräver också ett certifikat som kan köras på HTTPS i din utvecklingsmiljö.

Kör följande kommando.

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

Kommandot genererar en `key.pem`- och en `certificate.pem`-fil. Spara dessa filer i samma sökväg som din `universal-editor-service.cjs`-fil.

## Konfigurera tjänsten Universal Editor {#setting-up-service}

Ett antal miljövariabler måste anges i NodeJS för att den universella redigeringstjänsten ska kunna köras lokalt.

Skapa en `.env`-fil med följande innehåll på samma sökväg som dina `universal-editor-service.cjs`-, `key.pem`- och `certificate.pem`-filer.

```text
UES_PORT=8000
UES_PRIVATE_KEY=./key.pem
UES_CERT=./certificate.pem
UES_TLS_REJECT_UNAUTHORIZED=false
```

Detta är de minimivärden som krävs för lokal utveckling i vårt exempel. Följande tabell innehåller information om dessa och ytterligare värden.

| Värde | Valfritt | Standard | Beskrivning |
|---|---|---|---|
| `UES_PORT` | Ja | `8080` | Port som servern körs på |
| `UES_PRIVATE_KEY` | Ja | Ingen | Sökväg till den privata nyckeln för HTTPS-servern |
| `UES_CERT` | Ja | Ingen | Sökväg till certifieringsfilen för HTTPS-servern |
| `UES_TLS_REJECT_UNAUTHORIZED` | Ja | `true` | Avvisa obehöriga TLS-anslutningar |
| `UES_DISABLE_IMS_VALIDATION` | Ja | `false` | Inaktivera IMS-validering |
| `UES_ENDPOINT_MAPPING` | Ja | Tom | Mappning av slutpunkterna för interna omskrivningar<br>Exempel: `UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>Resultat: Universal Editor-tjänsten ansluter till `http://10.0.0.1:4502` i stället för den angivna anslutningen `https://your-public-facing-author-domain.net` |
| `UES_LOG_LEVEL` | Ja | `info` | Loggnivå för servern, möjliga värden är `silly`, `trace`, `debug`, `verbose`, `info`, `log`, `warn`, `error` och `fatal` |
| `UES_SPLUNK_HEC_URL` | Ja | Ingen | HEC URL till Splunk-slutpunkt |
| `UES_SPLUNK_TOKEN` | Ja | Ingen | Splunk-token |
| `UES_SPLUNK_INDEX` | Ja | Ingen | Index att skriva loggar till |
| `UES_SPLUNK_SOURCE` | Ja | `universal-editor-service` | Namnet på källan i skräppostloggarna |

>[!NOTE]
>
>Före [2024.08.13-versionen](/help/release-notes/universal-editor/current.md) av Universal Editor krävdes följande variabler i `.env`-filen. Dessa värden stöds fram till den 1 oktober 2024 för bakåtkompatibilitet.
>
>`EXPRESS_PORT=8000`
>`EXPRESS_PRIVATE_KEY=./key.pem`
>`EXPRESS_CERT=./certificate.pem`
>`NODE_TLS_REJECT_UNAUTHORIZED=0`

## Kör den universella redigeringstjänsten {#running-ue}

Kör följande kommando för att starta Universal Editor-tjänsten:

```text
$ node ./universal-editor-service.cjs
```

Följande bör skickas till din terminal:

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

Kontrollera att HTTPS-servern inte är en HTTP-server startas av tjänsten.

## Använda den lokala universella redigeringstjänsten i stället för den globala tjänsten {#using-local-ue}

Den universella redigeraren vet vilken Universal Editor-tjänst som ska användas för att redigera en sida baserat på hur sidan är instrumenterad. Detta görs via metataggar på sidan som läses in i Universal Editor.

För att en sida ska kunna redigeras med din lokala Universal Editor-tjänst måste följande meta-tagg anges:

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

När den är inställd ska du se alla anrop om innehållsuppdatering gå till `https://localhost:8000` i stället för standardtjänsten Universal Editor.

>[!NOTE]
>
>Om du försöker få direktåtkomst till `https://localhost:8000` uppstår ett `404`-fel. Detta är förväntat beteende.
>
>Använd `https://localhost:8000/corslib/LATEST` om du vill testa åtkomsten till den lokala Universal Editor-tjänsten. Mer information finns i [nästa avsnitt](#editing).

>[!TIP]
>
>Mer information om hur sidor instrumenteras för att använda den globala universella redigeringstjänsten finns i dokumentet [Komma igång med den universella redigeraren i AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Redigera en sida med den lokala universella redigeringstjänsten {#editing}

Med den [universella redigeringstjänsten som körs lokalt](#running-ue) och [innehållssidan som är instrumenterad för att använda den lokala tjänsten](#using-loca-ue) kan du nu starta redigeraren.

1. Öppna webbläsaren på `https://localhost:8000/corslib/LATEST`.
1. Be webbläsaren acceptera [ditt självsignerade certifikat.](#ue-https)
1. När det självsignerade certifikatet är betrott kan du redigera sidan med din lokala Universal Editor-tjänst.

