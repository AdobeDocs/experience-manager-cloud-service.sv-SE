---
title: Genererar åtkomsttoken för serversides-API:er (äldre)
description: Lär dig att underlätta kommunikationen mellan en tredjepartsserver och AEM as a Cloud Service genom att generera en säker JWT-token
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 0%

---

# Genererar åtkomsttoken för serversides-API:er (äldre) {#generating-access-tokens-for-server-side-apis-legacy}

Vissa arkitekturer förlitar sig på att ringa för att AEM as a Cloud Service från ett program som finns på en server utanför AEM infrastruktur. Ett mobilprogram som anropar en server, som sedan gör API-begäranden till AEM as a Cloud Service.

Flödet server-till-server beskrivs nedan tillsammans med ett förenklat utvecklingsflöde. AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) används för att generera tokens som behövs för autentiseringsprocessen.

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Server-till-server-flödet {#the-server-to-server-flow}

En användare med en IMS-organisationsadministratörsroll, och som även är medlem i produktprofilen AEM användare eller AEM administratörer på AEM Author, kan generera en AEM as a Cloud Service autentiseringsuppgift. Autentiseringsuppgifterna kan senare hämtas av en användare med AEM as a Cloud Service miljöadministratörsroll och bör installeras på servern och måste behandlas noggrant som en hemlig nyckel. Den här JSON-formatfilen innehåller alla data som behövs för att integrera med ett AEM as a Cloud Service API. Data används för att skapa en signerad JWT-token, som byts ut mot IMS för en IMS-åtkomsttoken. Denna åtkomsttoken kan sedan användas som en Bearer-autentiseringstoken för att göra förfrågningar till AEM as a Cloud Service. Autentiseringsuppgifterna går ut om ett år som standard, men de kan uppdateras vid behov enligt beskrivningen [här](#refresh-credentials).

Flödet server-till-server omfattar följande steg:

* Hämta autentiseringsuppgifterna för AEM as a Cloud Service från Developer Console
* Installera autentiseringsuppgifterna för AEM as a Cloud Service på en icke-AEM server som gör anrop till AEM
* Generera en JWT-token och byt ut denna token mot en åtkomsttoken med hjälp av Adobe IMS API:er
* Anropa AEM-API:t med åtkomsttoken som en Bearer-autentiseringstoken
* Ange lämplig behörighet för den tekniska kontoanvändaren i AEM

### Hämta AEM as a Cloud Service autentiseringsuppgifter {#fetch-the-aem-as-a-cloud-service-credentials}

Användare med tillgång till den AEM as a Cloud Service utvecklarkonsolen kan se integreringsfliken i Developer Console för en viss miljö och två knappar. En användare med AEM as a Cloud Service miljöadministratörsroll kan klicka på **Generera autentiseringsuppgifter för tjänsten** för att generera och visa tjänstens inloggningsuppgifter. JSON innehåller all information som krävs för den icke-AEM servern, inklusive klient-ID, klienthemlighet, privat nyckel, certifikat och konfiguration för utvecklings- och publiceringsnivåer i miljön, oavsett vilket pod som valts.

![JWT-generering](assets/JWTtoken3.png)

Utdata liknar följande:

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

När inloggningsuppgifterna har skapats kan de hämtas senare genom att trycka på **Hämta tjänstautentiseringsuppgifter** på samma plats.

>[!IMPORTANT]
>
>En IMS-organisationsadministratör, vanligtvis den användare som tilldelade miljön via Cloud Manager, som också ska vara medlem i produktprofilen AEM användare eller AEM administratörer på AEM Author, har åtkomst till Developer Console. Sedan måste de klicka på **Generera autentiseringsuppgifter för tjänsten** så att inloggningsuppgifterna genereras och hämtas senare av en användare med administratörsbehörighet till den AEM as a Cloud Service miljön. Om IMS-organisationsadministratören inte har gjort den här åtgärden får de ett meddelande om att de behöver rollen IMS-organisationsadministratör.

### Installera autentiseringsuppgifterna för AEM på en icke-AEM server {#install-the-aem-service-credentials-on-a-non-aem-server}

Det icke-AEM programmet som anropar AEM bör kunna få tillgång till inloggningsuppgifterna AEM as a Cloud Service, och behandla dem som en hemlighet.

### Generera en JWT-token och ersätt den för en åtkomsttoken {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Använd autentiseringsuppgifterna för att skapa en JWT-token i ett anrop till Adobe IMS-tjänsten för att hämta en åtkomsttoken, som är giltig i 24 timmar.

AEM CS Service Credentials kan bytas ut mot en åtkomsttoken med hjälp av klientbibliotek som är utformade för detta ändamål. Klientbiblioteken är tillgängliga från [Adobe allmänt GitHub-databas](https://github.com/adobe/aemcs-api-client-lib), som innehåller mer detaljerad vägledning och den senaste informationen.

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

Samma utbyte kan utföras på vilket språk som helst som kan generera en signerad JWT-token med rätt format och anropa API:erna för IMS Token Exchange.

Åtkomsttoken definierar när den upphör att gälla, vilket vanligtvis är 24 timmar. Det finns exempelkod i Git-databasen för att hantera en åtkomsttoken och uppdatera den innan den upphör att gälla.

### Anropa AEM API {#calling-the-aem-api}

Gör lämpliga server-till-server-API-anrop till en AEM as a Cloud Service miljö, inklusive åtkomsttoken i huvudet. Använd därför värdet för rubriken&quot;Authorization&quot; `"Bearer <access_token>"`. Använd till exempel `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Ange lämpliga behörigheter för den tekniska kontoanvändaren i AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

När den tekniska kontoanvändaren har skapats i AEM (inträffar efter den första begäran med motsvarande åtkomsttoken) måste den tekniska kontoanvändaren ha rätt behörighet **in** AEM.

I AEM Author-tjänsten läggs som standard den tekniska kontoanvändaren till i Contributors-användargruppen som tillhandahåller AEM.

Den här tekniska kontoanvändaren i AEM kan tilldelas ytterligare behörigheter med de vanliga metoderna.

## Utvecklarflöde {#developer-flow}

Utvecklare bör testa med hjälp av en utvecklingsinstans av sin icke-AEM applikation (antingen som körs på sin bärbara dator eller på sin värddator) som begär en utveckling AEM as a Cloud Service utvecklingsmiljö. Eftersom utvecklare inte nödvändigtvis har behörigheten IMS-administratörsroll kan Adobe inte anta att de kan generera JWT-bäraren som beskrivs i det vanliga server-till-server-flödet. Adobe tillhandahåller alltså en mekanism för en utvecklare att generera en åtkomsttoken direkt som kan användas i begäranden till en AEM as a Cloud Service miljö som de har tillgång till.

Se [Dokumentation till Developer Guidelines](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) om du vill ha information om de behörigheter som krävs för att använda den AEM as a Cloud Service utvecklarkonsolen.

>[!NOTE]
>
Åtkomsttoken för lokal utveckling är giltig i högst 24 timmar. Därefter måste den genereras om med samma metod.

Utvecklare kan använda denna token för att ringa anrop från andra testprogram än AEM till en AEM as a Cloud Service miljö. I vanliga fall använder utvecklaren denna token tillsammans med programmet som inte är AEM på sin egen bärbara dator. AEM som moln är vanligtvis en icke-produktionsmiljö.

Utvecklarflödet omfattar följande steg:

* Generera en åtkomsttoken från Developer Console
* Anropa AEM program med åtkomsttoken.

Utvecklare kan också göra API-anrop till ett AEM projekt som körs på deras lokala dator. I så fall behövs ingen åtkomsttoken.

### Genererar åtkomsttoken {#generating-the-access-token}

Om du vill generera en åtkomsttoken klickar du på Developer Console **Hämta lokal utvecklingstoken**.

### Anropa sedan AEM program med en åtkomsttoken {#call-the-aem-application-with-an-access-token}

Gör lämpliga server-till-server-API-anrop från det icke-AEM programmet till en AEM as a Cloud Service miljö, inklusive åtkomsttoken i huvudet. Använd därför värdet för rubriken&quot;Authorization&quot; `"Bearer <access_token>"`.

## Uppdatera autentiseringsuppgifter {#refresh-credentials}

Som standard går autentiseringsuppgifter på AEM as a Cloud Service ut efter ett år. För att säkerställa kontinuiteten i tjänsterna kan utvecklarna uppdatera sina autentiseringsuppgifter och förlänga tillgängligheten ytterligare ett år. Använd **Uppdatera autentiseringsuppgifter för tjänsten** från **Integreringar** på utvecklarkonsolen, enligt nedan.

![Uppdatera autentiseringsuppgifter](assets/credential-refresh.png)

När du har tryckt på knappen genereras en ny uppsättning med autentiseringsuppgifter. Du kan uppdatera din hemliga lagring med de nya autentiseringsuppgifterna och validera att de fungerar som de ska.

>[!NOTE]
>
När du klickat på **Uppdatera autentiseringsuppgifter för tjänsten** de gamla inloggningsuppgifterna är fortfarande registrerade tills de upphör att gälla, men endast den senaste uppsättningen är tillgänglig att se från Developer Console vid ett och samma tillfälle.

## Återkallande av tjänstautentiseringsuppgifter {#service-credentials-revocation}

Om inloggningsuppgifterna måste återkallas måste du skicka en förfrågan till kundsupport på följande sätt:

1. Inaktivera den tekniska kontoanvändaren för Adobe Admin Console i användargränssnittet:
   * I Cloud Manager trycker du på **...** -knapp bredvid din miljö. Den här åtgärden öppnar sidan med produktprofiler
   * Klicka på **AEM** profil, om du vill visa en lista med användare
   * Klicka på **API-autentiseringsuppgifter** och sedan hitta rätt kontoanvändare och ta bort den
2. Kontakta kundsupport och begär att tjänstens autentiseringsuppgifter för den specifika miljön tas bort
3. Slutligen kan du generera inloggningsuppgifterna igen enligt beskrivningen i den här dokumentationen. Se även till att den nya tekniska kontoanvändaren som skapas har rätt behörigheter.
