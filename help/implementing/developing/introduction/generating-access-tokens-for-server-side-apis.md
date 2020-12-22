---
title: Genererar åtkomsttoken för API:er på serversidan
description: Lär dig att underlätta kommunikationen mellan en tredjepartsserver och AEM som en Cloud Service genom att generera en säker JWT-token
translation-type: tm+mt
source-git-commit: 7ca7cd458ea5152d56754bf1e6a500b2c04d0039
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---


# Introduktion {#introduction}

>[!IMPORTANT]
>
>Den här funktionen är inte tillgänglig än. I [versionsinformationen](/help/release-notes/release-notes-cloud/release-notes-current.md) finns en aktuell lista över funktioner.

Vissa arkitekturer förlitar sig på att anropa AEM som Cloud Service från ett program som finns på en server utanför AEM infrastruktur. Ett mobilprogram som anropar en server, som sedan gör API-begäranden till AEM som en Cloud Service.

Flödet server-till-server beskrivs nedan tillsammans med ett förenklat utvecklingsflöde. AEM som Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) används för att generera tokens som behövs för autentiseringsprocessen.

## Server-till-server-flödet {#the-server-to-server-flow}

En användare med administratörsrollen kan generera en AEM som en Cloud Service-autentiseringsuppgift, som ska vara installerad på servern och behandlas noggrant som en hemlig nyckel. Den här JSON-formatfilen innehåller alla data som behövs för att integrera med en AEM som Cloud Service-API. Data används för att skapa en signerad JWT-token, som byts ut mot IMS för en IMS-åtkomsttoken. Denna åtkomsttoken kan sedan användas som en Bearer-autentiseringstoken för att göra begäranden till AEM som Cloud Service.

Flödet server-till-server omfattar följande steg:

* Hämta AEM som en Cloud Service-autentiseringsuppgifter från Developer Console
* Installera AEM som en Cloud Service på en icke-AEM server som gör anrop till AEM
* Generera en JWT-token och byt ut denna token mot en åtkomsttoken med hjälp av Adobe IMS API:er
* Anropa AEM-API:t med åtkomsttoken som en Bearer-autentiseringstoken

### Hämta AEM som Cloud Service-autentiseringsuppgifter {#fetch-the-aem-as-a-cloud-service-credentials}

Användare som har administratörsrollen för en IMS-organisation kan se integreringsfliken i Developer Console för en viss miljö, samt två knappar. Om du klickar på knappen **Hämta tjänstinloggningsuppgifter** skapas tjänstens inloggningsuppgifter (json), som innehåller all information som krävs för den icke-AEM servern, inklusive klient-ID, klienthemlighet, privat nyckel, certifikat och konfiguration för utvecklings- och publiceringsnivåer i miljön, oavsett vilket pod som valts.

![JWT-generering](assets/JWTtoken3.png)

Utdata kommer att se ut ungefär så här:

```
{
  "ok": true,
  "integration": {
    "imsEndpoint": "ims-na1.adobelogin.com",
    "metascopes": "ent_aem_cloud_sdk,ent_cloudmgr_sdk",
    "technicalAccount": {
      "clientId": "cm-p123-e1234",
      "clientSecret": "4AREDACTED17"
    },
    "email": "abcd@techacct.adobe.com",
    "id": "ABCDAE10A495E8C@techacct.adobe.com",
    "org": "1234@AdobeOrg",
    "privateKey": "-----BEGIN RSA PRIVATE KEY-----\r\REDACTED\r\n==\r\n-----END RSA PRIVATE KEY-----\r\n",
    "publicKey": "-----BEGIN CERTIFICATE-----\r\nREDACTED\r\n-----END CERTIFICATE-----\r\n"
  },
  "statusCode": 200
}
```

### Installera autentiseringsuppgifterna för AEM på en icke-AEM server {#install-the-aem-service-credentials-on-a-non-aem-server}

Det icke-AEM programmet som anropar AEM bör kunna komma åt AEM som en Cloud Service och behandla den som en hemlighet.

### Generera en JWT-token och ersätt den för en åtkomsttoken{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Använd autentiseringsuppgifterna för att skapa en JWT-token i ett anrop till Adobe IMS-tjänsten för att hämta en åtkomsttoken, som är giltig i 24 timmar.

AEM-CS Service Credentials kan bytas ut mot en åtkomsttoken med hjälp av klientbibliotek som är utformade för detta ändamål. Klientbiblioteken är tillgängliga från [Adobe offentlig GitHub-databas](https://github.com/adobe/aemcs-api-client-lib), som innehåller mer detaljerad vägledning och senaste information.

```
/*jshint node:true */
"use strict";

const fs = require('fs');
const exchange = require("@adobe/aemcs-api-client-lib");

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

Samma utbyte kan utföras på alla språk som kan generera en signerad JWT-token med rätt format och anropa API:erna för IMS Token Exchange.

Åtkomsttoken definierar när den upphör att gälla, vilket vanligtvis är 12 timmar. Det finns exempelkod i Git-databasen för att hantera en åtkomsttoken och uppdatera den innan den upphör att gälla.

### Anropa AEM-API {#calling-the-aem-api}

Gör lämpliga server-till-server-API-anrop till en AEM som en Cloud Service, inklusive åtkomsttoken i huvudet. Använd därför värdet `"Bearer <access_token>"` för auktoriseringshuvudet. Använd till exempel `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

## Utvecklarflöde {#developer-flow}

Utvecklare kommer troligen att vilja testa med hjälp av en utvecklingsinstans av sin icke-AEM-programvara (som antingen körs på deras bärbara dator eller på deras värddator) som gör begäranden till en AEM som en Cloud Service-utvecklingsmiljö. Eftersom utvecklare inte nödvändigtvis har administratörsrollåtkomst till AEM som en Cloud Service dev-miljö, kan vi inte anta att de kan generera JWT-bäraren som beskrivs i det vanliga server-till-server-flödet. Därför erbjuder vi en mekanism för en utvecklare att generera en åtkomsttoken direkt som kan användas i begäranden som AEM som en Cloud Service som de har tillgång till. I [dokumentationen till Utvecklarriktlinjer](/help/implementing/developing/introduction/development-guidelines.md) finns information om vilka behörigheter som krävs för att använda AEM som Cloud Service-utvecklarkonsol.

>[!NOTE]
>
>Token gäller i 24 timmar. Därefter måste den genereras om med samma metod.

Utvecklare kan använda denna token för att ringa anrop från andra program än AEM till en AEM som en Cloud Service. I vanliga fall använder utvecklaren denna token tillsammans med programmet som inte är AEM på sin egen bärbara dator. AEM som moln är vanligtvis en icke-produktionsmiljö.

Utvecklarflödet omfattar följande steg:

* Generera en åtkomsttoken från Developer Console
* Anropa AEM program med åtkomsttoken.

Utvecklare kan också göra API-anrop till ett AEM projekt som körs på deras lokala dator. I så fall behövs ingen åtkomsttoken.

### Genererar åtkomsttoken {#generating-the-access-token}

Klicka på knappen **Hämta lokal utvecklingstoken** i Developer Console för att generera en åtkomsttoken.

### Anropa sedan AEM programmet med en åtkomsttoken {#call-the-aem-application-with-an-access-token}

Gör lämpliga server-till-server-API-anrop från det icke-AEM programmet till en AEM som en Cloud Service, inklusive åtkomsttoken i huvudet. Använd därför värdet `"Bearer <access_token>"` för auktoriseringshuvudet.

## Återkallning av tjänstens autentiseringsuppgifter {#service-credentials-revocation}

Skicka en förfrågan till kundsupport om JWT Bearer-token måste återkallas.