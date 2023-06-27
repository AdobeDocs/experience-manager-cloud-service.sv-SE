---
title: Genererar åtkomsttoken för API:er på serversidan
description: Lär dig att underlätta kommunikationen mellan en tredjepartsserver och AEM as a Cloud Service genom att generera en säker JWT-token
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '2090'
ht-degree: 0%

---

# Genererar åtkomsttoken för API:er på serversidan {#generating-access-tokens-for-server-side-apis}

Vissa arkitekturer förlitar sig på att ringa för att AEM as a Cloud Service från ett program som finns på en server utanför AEM infrastruktur. Ett mobilprogram som anropar en server, som sedan gör API-begäranden till AEM as a Cloud Service.

Flödet server-till-server beskrivs nedan tillsammans med ett förenklat utvecklingsflöde. AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) används för att generera tokens som behövs för autentiseringsprocessen.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## Server-till-server-flödet {#the-server-to-server-flow}

Användare med en IMS-organisationsadministratörsroll, och som är medlem i produktprofilen AEM användare eller AEM administratörer på AEM Author, kan generera en uppsättning inloggningsuppgifter från AEM as a Cloud Service. Varje referens är en JSON-nyttolast som innehåller ett certifikat (den offentliga nyckeln), en privat nyckel och ett tekniskt konto som består av en `clientId` och `clientSecret`. Dessa autentiseringsuppgifter kan senare hämtas av en användare med AEM as a Cloud Service miljöadministratörsroll och bör installeras på en icke-AEM server och behandlas noggrant som en hemlig nyckel. Den här JSON-formatfilen innehåller alla data som behövs för att integrera med ett AEM as a Cloud Service API. Data används för att skapa en signerad JWT-token, som byts med Adobe Identity Management Services (IMS) för en IMS-åtkomsttoken. Denna åtkomsttoken kan sedan användas som en Bearer-autentiseringstoken för att göra förfrågningar till AEM as a Cloud Service. Certifikatet i inloggningsuppgifterna upphör att gälla efter ett år som standard, men de kan uppdateras vid behov enligt beskrivningen [här](#refresh-credentials).

Flödet server-till-server omfattar följande steg:

* Hämta autentiseringsuppgifterna på AEM as a Cloud Service från Developer Console
* Installera autentiseringsuppgifterna för AEM as a Cloud Service på en icke-AEM server som gör anrop till AEM
* Generera en JWT-token och byt ut denna token mot en åtkomsttoken med hjälp av Adobe IMS API:er
* Anropa AEM-API:t med åtkomsttoken som en Bearer-autentiseringstoken
* Ange lämplig behörighet för den tekniska kontoanvändaren i AEM

### Hämta AEM as a Cloud Service autentiseringsuppgifter {#fetch-the-aem-as-a-cloud-service-credentials}

Användare med tillgång till den AEM as a Cloud Service utvecklarkonsolen kan se integreringsfliken i Developer Console för en viss miljö. En användare med administratörsrollen AEM as a Cloud Service Environment kan skapa, visa och hantera autentiseringsuppgifter.

Klicka **Skapa nytt tekniskt konto** skapas en uppsättning autentiseringsuppgifter som innehåller klient-ID, klienthemlighet, privat nyckel, certifikat och konfiguration för utvecklings- och publiceringsnivåer i miljön, oavsett vilket pod-val som har gjorts.

![Skapa ett nytt tekniskt konto](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

En ny flik i webbläsaren öppnas och inloggningsuppgifterna visas. Du kan använda den här vyn för att hämta inloggningsuppgifterna genom att trycka på nedladdningsikonen bredvid statustiteln:

![Hämta autentiseringsuppgifter](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

När inloggningsuppgifterna har skapats visas de under **Tekniska konton** i **Integreringar** avsnitt:

![Visa autentiseringsuppgifter](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Användarna kan senare visa inloggningsuppgifterna med åtgärden Visa. Dessutom kan användare redigera inloggningsuppgifterna för samma tekniska konto, vilket beskrivs senare i artikeln. De gör den här redigeringen genom att skapa en ny privat nyckel eller ett certifikat, i de fall då certifikatet måste förnyas eller återkallas.

Användare med rollen AEM as a Cloud Service miljöadministratör kan senare skapa autentiseringsuppgifter för ytterligare tekniska konton. Den här funktionen är användbar när olika API:er har olika åtkomstkrav. Till exempel läs kontra läs/skriv.

>[!NOTE]
>
>Kunder kan skapa upp till tio tekniska konton, inklusive konton som redan har tagits bort.

>[!IMPORTANT]
>
>En IMS-organisationsadministratör (vanligtvis samma användare som provisionerade miljön via Cloud Manager), som också är medlem i produktprofilen AEM användare eller AEM administratörer för AEM-författare, måste först få åtkomst till Developer Console. Klicka sedan på **Skapa nytt tekniskt konto** för de autentiseringsuppgifter som ska genereras och senare hämtas av en användare med administratörsbehörighet till den AEM as a Cloud Service miljön. Om IMS-organisationsadministratören inte har skapat det tekniska kontot än visas ett meddelande om att de behöver rollen IMS-organisationsadministratör.

### Installera autentiseringsuppgifterna för AEM på en icke-AEM server {#install-the-aem-service-credentials-on-a-non-aem-server}

Programmet som anropar AEM bör kunna komma åt inloggningsuppgifterna för AEM as a Cloud Service och behandla dem som en hemlighet.

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

>[!NOTE]
>Om det finns flera inloggningsuppgifter måste du referera till rätt JSON-fil för API-anropet till AEM som anropas senare.

### Anropa AEM API {#calling-the-aem-api}

Gör lämpliga server-till-server-API-anrop till en AEM as a Cloud Service miljö, inklusive åtkomsttoken i huvudet. Använd därför värdet för rubriken&quot;Authorization&quot; `"Bearer <access_token>"`. Använd till exempel `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Ange lämpliga behörigheter för den tekniska kontoanvändaren i AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Först måste en ny produktprofil skapas i Adobe Admin Console.

1. Gå till Adobe Admin Console på [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).
1. Tryck på **Hantera** länk under **Produkter och tjänster** till vänster.
1. Välj **AEM as a Cloud Service**.
1. Tryck på **Ny profil** -knappen.

   ![Ny profil](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Namnge profilen och tryck på **Spara**.

   ![Spara profil](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Välj den profil som du skapade i profillistan.
1. Välj **Lägg till användare**.

   ![Lägg till användare](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Lägg till det tekniska konto som du skapade (i det här fallet) `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) och klicka på **Spara**.

   ![Lägg till teknikkonto](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. Vänta i 10 minuter tills ändringarna börjar gälla och gör ett API-anrop till AEM med en åtkomsttoken som genererats från den nya autentiseringsuppgiften. Som ett cURL-kommando motsvaras det av följande exempel:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


När du har gjort API-anropet visas produktprofilen som en användargrupp i den AEM as a Cloud Service författarinstansen, med lämpligt tekniskt konto som medlem i den gruppen.

Så här kontrollerar du informationen:

1. Logga in på författarinstansen.
1. Gå till **verktyg** > **Säkerhet** klickar du på **Grupper** kort.
1. Leta reda på namnet på profilen som du skapade i listan med grupper och klicka på den:

   ![Gruppprofil](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. I följande fönster växlar du till **Medlemmar** tabba och kontrollera om det tekniska kontot finns korrekt i listan:

   ![Fliken Medlemmar](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


Du kan också verifiera att det tekniska kontot visas i användarlistan genom att utföra följande steg på författarinstansen:

1. Gå till **verktyg** > **Säkerhet** > **Användare**.
1. Kontrollera att ditt tekniska konto är användarlistan och välj det.
1. Klicka på **Grupper** så att du kan verifiera att användaren är en del av gruppen som motsvarar din produktprofil. Den här användaren ingår även i en handfull andra grupper, bland annat följande:

   ![Gruppmedlemskap](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Före mitten av 2023, innan det var möjligt att skapa flera autentiseringsuppgifter, vägleddes kunderna inte att skapa en produktprofil i Adobe Admin Console. Det tekniska kontot var därför inte kopplat till någon annan grupp än&quot;Medarbetare&quot; i den AEM as a Cloud Service instansen. Av konsekvensskäl rekommenderar vi att du skapar en produktprofil i Adobe Admin Console enligt beskrivningen ovan och lägger till den befintliga tekniska redovisningen i den gruppen.

<u>**Ange lämpliga gruppbehörigheter**</u>

Slutligen måste du konfigurera gruppen med de behörigheter som krävs så att du kan anropa eller låsa API:erna korrekt.

1. Logga in på rätt författarinstans och navigera till **Inställningar** > **Säkerhet** > **Behörigheter**
1. Sök efter namnet på gruppen som motsvarar produktprofilen i den vänstra rutan (i det här fallet skrivskyddade API:er) och markera den:

   ![Sök efter grupp](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Klicka på knappen Redigera i följande fönster:

   ![Redigera behörigheter](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Ändra behörigheterna korrekt och klicka på **Spara**

   ![Bekräfta redigering av behörigheter](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Läs mer om Adobe Identity Management System (IMS) och AEM användare och grupper. Se [dokumentation](/help/security/ims-support.md).

## Utvecklarflöde {#developer-flow}

Utvecklare vill antagligen testa med en utvecklingsinstans av sina icke-AEM program (som antingen körs på bärbara datorer eller på värdtjänster) som begär en utveckling AEM as a Cloud Service utvecklingsmiljö. Eftersom utvecklare inte nödvändigtvis har behörigheten IMS-administratörsroll kan Adobe inte anta att de kan generera JWT-bäraren som beskrivs i det vanliga server-till-server-flödet. Därför erbjuder Adobe en mekanism för en utvecklare att generera en åtkomsttoken direkt som kan användas i begäranden till miljöer på AEM as a Cloud Service som de har tillgång till.

Se [Dokumentation till Developer Guidelines](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) om du vill ha information om de behörigheter som krävs för att använda den AEM as a Cloud Service utvecklarkonsolen.

>[!NOTE]
>
>Åtkomsttoken för lokal utveckling är giltig i högst 24 timmar. Därefter måste den genereras om med samma metod.

Utvecklare kan använda denna token för att ringa anrop från andra testprogram än AEM till en AEM as a Cloud Service miljö. I vanliga fall använder utvecklaren denna token tillsammans med programmet som inte är AEM på sin egen bärbara dator. AEM som moln är vanligtvis en icke-produktionsmiljö.

Utvecklarflödet omfattar följande steg:

* Generera en åtkomsttoken från Developer Console
* Anropa AEM program med åtkomsttoken.

Utvecklare kan också göra API-anrop till ett AEM projekt som körs på deras lokala dator. I så fall behövs ingen åtkomsttoken.

### Genererar åtkomsttoken {#generating-the-access-token}

1. Gå till **Lokal token** under **Integreringar**
1. Klicka **Hämta lokal utvecklingstoken** i Developer Console så att du kan generera en åtkomsttoken.

### Anropa AEM program med en åtkomsttoken {#call-the-aem-application-with-an-access-token}

Gör lämpliga server-till-server-API-anrop från det icke-AEM programmet till en AEM as a Cloud Service miljö, inklusive åtkomsttoken i huvudet. Använd därför värdet för rubriken&quot;Authorization&quot; `"Bearer <access_token>"`.

## Uppdatera autentiseringsuppgifter {#refresh-credentials}

Som standard upphör inloggningsuppgifterna på AEM as a Cloud Service att gälla efter ett år. För att säkerställa kontinuiteten i tjänsterna kan utvecklarna uppdatera sina autentiseringsuppgifter och förlänga tillgängligheten ytterligare ett år.

Så här uppnår du det här uppdateringstillägget:

* Använd **Lägg till certifikat** knapp under **Integreringar** - **Tekniska konton** i Developer Console, som visas nedan

  ![Uppdatera autentiseringsuppgifter](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* När du har tryckt på knappen genereras en uppsättning autentiseringsuppgifter som innehåller ett nytt certifikat. Installera de nya autentiseringsuppgifterna på den AEM servern och kontrollera att anslutningen fungerar som förväntat, utan att ta bort de gamla autentiseringsuppgifterna.
* Kontrollera att de nya autentiseringsuppgifterna används i stället för de gamla när du genererar åtkomsttoken.
* Du kan också återkalla (och sedan ta bort) det tidigare certifikatet så att det inte längre kan användas för att autentisera med AEM as a Cloud Service.

## Återkallande av autentiseringsuppgifter {#credentials-revocation}

Om den privata nyckeln komprometteras måste du skapa autentiseringsuppgifter med ett nytt certifikat och en ny privat nyckel. När ditt program har använt de nya autentiseringsuppgifterna så att du kan generera åtkomsttoken kan du återkalla och ta bort de gamla certifikaten genom att göra följande:

1. Lägg först till den nya nyckeln. Den här nyckeln genererar autentiseringsuppgifter med en ny privat nyckel och ett nytt certifikat. Den nya privata nyckeln markeras som **aktuell** och används därför för alla nya autentiseringsuppgifter för det här tekniska kontot. Autentiseringsuppgifterna som är associerade med de äldre privata nycklarna är fortfarande giltiga tills de återkallas. Markera tre punkter för att få detta återkallande (**...**) under ditt nuvarande tekniska konto och sedan väljer **Lägg till ny privat nyckel**:

   ![Lägg till ny privat nyckel](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Välj **Lägg till** vid uppmaningen som följer:

   ![Bekräfta tillägg av ny privat nyckel](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   En ny bläddringsflik med de nya inloggningsuppgifterna öppnas och användargränssnittet uppdateras så att både privata nycklar visas med den nya som markerats som **aktuell**:

   ![Privata nycklar i användargränssnittet](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. Installera de nya autentiseringsuppgifterna på den icke-AEM servern och kontrollera att anslutningen fungerar som förväntat. Se [Avsnittet Server-till-server-flöde](#the-server-to-server-flow) för mer information.
1. Återkalla det gamla certifikatet genom att välja tre punkter (**...**) till höger om certifikatet och välja **Återkalla**:

   ![Återkalla certifikat](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   Bekräfta sedan återkallningen i följande dialogruta genom att trycka på **Återkalla** knapp:

   ![Återkalla certifikatbekräftelse](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Slutligen tar du bort det skadade certifikatet.
