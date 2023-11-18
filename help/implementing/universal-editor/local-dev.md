---
title: Local AEM Development with the Universal Editor
description: Läs om hur den universella redigeraren stöder redigering i lokala AEM för utvecklingsändamål.
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Local AEM Development with the Universal Editor {#local-dev-ue}

Läs om hur den universella redigeraren stöder redigering i lokala AEM för utvecklingsändamål.

Det här dokumentet förklarar hur du kör AEM i HTTPS tillsammans med en lokal kopia av Universal Editor-tjänsten så att du kan utveckla lokalt på AEM med Universal Editor.

## Konfigurera AEM som ska köras på HTTPS {#aem-https}

I en yttre ram som skyddas med HTTPS kan en osäker HTTP-ram inte läsas in. Tjänsten Universal Editor körs på HTTPS och därför måste AEM eller andra fjärrsidor också köras på HTTPS.

För att göra detta måste du konfigurera AEM för att köra HTTPS. I utvecklingssyfte kan du använda självsignerade certifikat.

Se det här dokumentet om hur du konfigurerar AEM som körs på HTTPS med ett självsignerat certifikat som du kan använda.

## Installera Universal Editor-tjänsten {#install-ue-service}

Universal Editor-tjänsten är den som binder Universal Editor och serverdelssystemet. Eftersom den officiella universella redigeringstjänsten finns på en global värd måste den lokala AEM exponeras för Internet. Du kan undvika detta genom att köra en lokal kopia av Universal Editor-tjänsten.

[NodeJS version 16](https://nodejs.org/en/download/releases) krävs för att köra en lokal kopia av Universal Editor-tjänsten

Tjänsten Universal Editor distribueras direkt av AEM Engineering. Kontakta teknikern i VIP program för en lokal kopia.

Teknikern ger dig en `universal-editor-service.cjs` -fil. Spara detta i den lokala utvecklingsmiljön.

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

```
<meta name="urn:adobe:aem:editor:endpoint" content="https://localhost:8000">
```

När du väl har angett det ska du se varje anrop till innehållsuppdatering gå till `https://localhost:8000` i stället för standardtjänsten Universal Editor.

>[!TIP]
>
>Mer information om hur sidorna är instrumenterade för att använda den globala redigeringstjänsten finns i dokumentet [Komma igång med Universal Editor i AEM](/help/implementing/universal-editor/getting-started.md#instrument-page)

## Redigera en sida med den lokala universella redigeringstjänsten {#editing}

Med [Universell redigeringstjänst som körs lokalt](#running-ue) och [Innehållssida som är instrumenterad för att använda den lokala tjänsten.](#using-loca-ue) du kan nu starta redigeraren.

1. Öppna webbläsaren för att `https://localhost:8000/`.
1. Be webbläsaren godkänna [ditt självsignerade certifikat.](#ue-https)
1. När det självsignerade certifikatet är betrott kan du redigera sidan med din lokala Universal Editor-tjänst.
