---
title: Genererar åtkomsttoken för API:er på serversidan
description: Lär dig att underlätta kommunikationen mellan en tredjepartsserver och AEM som en Cloud Service genom att generera en säker JWT-token
translation-type: tm+mt
source-git-commit: 9a4cb6d981fdf5eea4d1b9c7ae9e3c99947d9745
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---


# Introduktion {#introduction}

>[!IMPORTANT]
>
>Den här funktionen är inte tillgänglig än. I [versionsinformationen](/help/release-notes/release-notes-cloud/release-notes-current.md) finns en aktuell lista över funktioner.

Vissa arkitekturer förlitar sig på att anropa AEM som Cloud Service från ett program som finns på en server utanför AEM infrastruktur. Ett mobilprogram som anropar en server, som sedan gör API-begäranden till AEM som en Cloud Service.

Flödet server-till-server beskrivs nedan tillsammans med ett förenklat utvecklingsflöde. AEM som Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) används för att generera tokens som behövs för autentiseringsprocessen.

## Server-till-server-flödet {#the-server-to-server-flow}

En användare med administratörsrollen kan generera en JWT-innehavartoken, som ska vara installerad på servern och behandlas noggrant som en hemlig nyckel. JWT Bärartoken bör bytas ut mot IMS för en åtkomsttoken, som ska inkluderas i begäran om att AEM som Cloud Service.

Flödet server-till-server omfattar följande steg:

* Generera JWT Ber-token från utvecklarkonsolen
* Installera token på en icke-AEM server som gör anrop till AEM
* Byt JWT Bearer-token för en åtkomsttoken med hjälp av Adobe IMS API:er
* Anropa AEM API

### Genererar JWT Bearer-token {#generating-the-jwt-bearer-token}

Användare som har administratörsrollen för en organisation kan se integreringsfliken i utvecklarkonsolen för en viss miljö, samt två knappar. Om du klickar på knappen **Hämta inloggningsuppgifter** skapas den privata nyckeln, certifikatet och konfigurationen.

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

### Installera token på en icke-AEM server {#install-the-token-on-a-non-aem-server}

Det icke-AEM programmet som anropar AEM bör installera JWT Ber-token och behandla det som en hemlighet.

### Byt ut JWT-token för en åtkomsttoken {#exchange-the-jwt-token-for-an-access-token}

Inkludera JWT-token i ett anrop till Adobe IMS-tjänsten för att hämta en åtkomsttoken, som är giltig i 24 timmar.

### Anropa AEM-API {#calling-the-aem-api}

Gör lämpliga server-till-server-API-anrop till en AEM som en Cloud Service, inklusive åtkomsttoken i huvudet. Använd därför värdet `"Bearer <access_token>"` för auktoriseringshuvudet.

<!-- ### Code Samples {#code-samples}

https://git.corp.adobe.com/boston/skyline-api-client-lib (internal note: URL will change to public git repo before we publish) contains client libraries written in node.js that will exchange the JSON outputted by the developer console for an access token. -->

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

## JWT Bearer Token Revocation {#jwt-bearer-token-revocation}

Skicka en förfrågan till kundsupport om JWT Bearer-token måste återkallas.