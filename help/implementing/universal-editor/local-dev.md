---
title: Local AEM Development with the Universal Editor
description: Läs om hur den universella redigeraren stöder redigering i lokala AEM för utvecklingsändamål.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: 422b4d98e2665e332ff65a3638a02282064b2bea
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---


# Local AEM Development with the Universal Editor {#local-dev-ue}

Läs om hur den universella redigeraren stöder redigering i lokala AEM för utvecklingsändamål.

{{universal-editor-status}}

## Ökning {#overview}

Universal Editor-tjänsten är den som binder Universal Editor och serverdelssystemet. Om du vill kunna utveckla lokalt för den universella redigeraren måste du köra en lokal kopia av den universella redigeringstjänsten. Detta beror på:

* Adobe officiella universell redigeringstjänst finns på en global värdserver och din lokala AEM måste vara exponerad för Internet.
* När du utvecklar med en lokal AEM SDK går det inte att komma åt Adobe universella redigeringstjänst från Internet.
* Om din AEM har IP-begränsningar och Adobe Universal Editor-tjänsten inte har ett definierat IP-intervall kan du själv vara värd för den.

I det här dokumentet förklaras hur du kör AEM i HTTPS tillsammans med en lokal kopia av Universal Editor-tjänsten så att du kan utveckla lokalt på AEM för användning med Universal Editor.

## Konfigurera AEM som ska köras på HTTPS {#aem-https}

I en yttre ram som skyddas med HTTPS går det inte att läsa in en osäker HTTP-ram. Tjänsten Universal Editor körs på HTTPS och därför måste AEM eller andra fjärrsidor också köras på HTTPS.

För att göra detta måste du konfigurera AEM för att köra HTTPS. I utvecklingssyfte kan du använda självsignerade certifikat.

[Se det här dokumentet](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html) om hur du konfigurerar AEM som körs på HTTPS med ett självsignerat certifikat som du kan använda.

## Installera Universal Editor-tjänsten {#install-ue-service}

Den universella redigeringstjänsten är inte en fullständig kopia av den universella redigeraren, utan bara en delmängd av dess funktioner för att säkerställa att samtal från den lokala AEM inte dirigeras över Internet, utan från en definierad slutpunkt som du kontrollerar.

[NodeJS version 16](https://nodejs.org/en/download/releases) krävs för att köra en lokal kopia av Universal Editor-tjänsten.

Tjänsten Universal Editor är tillgänglig via Software Distribution. Se [Dokumentation om programvarudistribution](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html) om du vill ha information om hur du får tillgång till den.

Spara `universal-editor-service.cjs` från Software Distribution till din lokala utvecklingsmiljö.

## Skapa ett certifikat som kör den universella redigeringstjänsten med HTTPS {#ue-https}

Tjänsten Universal Editor kräver också ett certifikat som kan köras på HTTPS i din utvecklingsmiljö.

Kör följande kommando.

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

Kommandot genererar en `key.pem` och `certificate.pem` -fil. Spara dessa filer i samma sökväg som `universal-editor-service.cjs` -fil.

## Konfigurera Universal Editor Service-konfigurationen {#setting-up-service}

Ett antal miljövariabler måste anges i NodeJS för att den universella redigeringstjänsten ska kunna köras lokalt.

På samma bana som `universal-editor-service.cjs`, `key.pem` och `certificate.pem` filer, skapa `.env` -fil med följande innehåll.

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

Variabeln har följande betydelse:

* `EXPRESS_PORT`: Definierar på vilken port Universal Editor-tjänsten lyssnar
* `EXPRESS_PRIVATE`: Peka på [tidigare skapad privat nyckel,](#ue-https) `key.pem`
* `EXPRESS_CERT`: Peka på [tidigare skapat certifikat,](#ue-https) `certificate.pem`
* `NODE_TLS_REJECT_UNAUTHORIZED=0`: Accepterar självsignerade certifikat

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

När du väl har angett det ska du se varje anrop till innehållsuppdatering gå till `https://localhost:8000` i stället för standardtjänsten Universal Editor.

>[!NOTE]
>
>Försöker få direktåtkomst `https://localhost:8000` resulterar i `404` fel. Detta är förväntat beteende.
>
>Om du vill testa åtkomsten till den lokala Universal Editor-tjänsten använder du `https://localhost:8000/corslib/LATEST`. Se [nästa avsnitt](#editing) för mer information.

>[!TIP]
>
>Mer information om hur sidorna är instrumenterade för att använda den globala redigeringstjänsten finns i dokumentet [Komma igång med Universal Editor i AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Redigera en sida med den lokala universella redigeringstjänsten {#editing}

Med [Universell redigeringstjänst som körs lokalt](#running-ue) och [Innehållssida som är instrumenterad för att använda den lokala tjänsten.](#using-loca-ue) du kan nu starta redigeraren.

1. Öppna webbläsaren för att `https://localhost:8000/corslib/LATEST`.
1. Be webbläsaren godkänna [ditt självsignerade certifikat.](#ue-https)
1. När det självsignerade certifikatet är betrott kan du redigera sidan med din lokala Universal Editor-tjänst.
