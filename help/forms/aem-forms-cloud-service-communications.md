---
title: AEM Forms as a Cloud Service - kommunikation
description: Sammanfoga data automatiskt med XDP- och PDF-mallar eller generera utdata i formaten PCL, ZPL och PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 20e54ff697c0dc7ab9faa504d9f9e0e6ee585464
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---


# Använd synkron bearbetning {#sync-processing-introduction}

Forms as a Cloud Service - Med API:er för kommunikation kan ni skapa, sammanställa och leverera varumärkesorienterad och personaliserad kommunikation som affärskorrespondenser, dokument, kontoutdrag, kravbrev, förmånsmeddelanden, kravbrev, månadsräkningar och välkomstpaket. Du kan använda API:er för kommunikation för att kombinera en mall (XFA eller PDF) med kunddata för att generera dokument i formaten PDF, PS, PCL, DPL, IPL och ZPL.

Tänk dig ett scenario där du har en eller flera mallar och flera poster med XML-data för varje mall. Du kan använda API:er för kommunikation för att generera ett utskriftsdokument för varje post. <!-- You can also combine the records into a single document. --> Resultatet är ett icke-interaktivt PDF-dokument. Ett icke-interaktivt PDF-dokument tillåter inte att användare anger data i sina fält.

Forms as a Cloud Service - Communications innehåller on demand- och batch-API:er (asynkrona API:er) för schemalagd dokumentgenerering:

* Synkrona API:er är lämpliga för dokumentgenerering on demand, med låg latens och en post. Dessa API:er lämpar sig bättre för användaråtgärdsbaserade användningsfall. Du kan till exempel skapa ett dokument när en användare har fyllt i ett formulär.

* API:er för gruppbearbetning (asynkrona API:er) är lämpliga för schemalagd hög genomströmning vid användning av flera dokumentgenereringar. Dessa API:er genererar dokument gruppvis. Till exempel telefonräkningar, kreditkortsräkningar och förmånsräkningar som genereras varje månad.

## Använd synkrona åtgärder {#batch-operations}

En synkron åtgärd är en process där dokument genereras linjärt. Dessa API:er klassificeras som single-tenant-API:er och multi-tenant-API:er:

### Single-tenant-API:er

* API:er för dokumentgenerering
* API:er för dokumentbearbetning

### API:er för flera innehavare

* API:er för dokumentverktyg

### Autentisera ett single-tenant-API

API-åtgärder för en innehavare har stöd för två typer av autentisering:

* **Grundläggande autentisering**: Grundläggande autentisering är ett enkelt autentiseringsschema som är inbyggt i HTTP-protokollet. Klienten skickar HTTP-begäranden med auktoriseringshuvudet som innehåller ordet Basic följt av ett blanksteg och en base64-kodad sträng med användarnamn:password. Om du till exempel vill auktorisera som administratör/administratör skickar klienten Basic [base64-kodad stränganvändarnamn]: [base64-kodat stränglösenord].

* **Tokenbaserad autentisering:** Tokenbaserad autentisering använder en åtkomsttoken (Bearer-autentiseringstoken) för att göra begäranden till Experience Manager as a Cloud Service. AEM Forms as a Cloud Service tillhandahåller API:er för att på ett säkert sätt hämta åtkomsttoken. Så här hämtar och använder du token för att autentisera en begäran:

   1. [Hämta as a Cloud Service autentiseringsuppgifter för Experience Manager från Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Installera as a Cloud Service autentiseringsuppgifter för Experience Manager i din miljö](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Programserver, webbserver eller andra icke-AEM servrar) som konfigurerats för att skicka begäranden till (ringa anrop) molntjänsten.
   1. [Generera en JWT-token och ersätt den med Adobe IMS API:er för en åtkomsttoken](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Kör Experience Manager-API:t med åtkomsttoken som en Bearer-autentiseringstoken.
   1. [Ange lämplig behörighet för den tekniska kontoanvändaren i Experience Manager-miljön](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe rekommenderar att du använder tokenbaserad autentisering i en produktionsmiljö.

### Autentisera ett multi-tenant-API

#### Autentiseringshuvuden

Alla inkommande HTTP API-anrop till Cloud Manager API måste innehålla följande tre rubriker:

* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

Värdena som ska skickas i `x-api-key` och `x-gw-ims-org-id` rubriker finns på skärmen Information om autentiseringsuppgifter i [Adobe Developer Console](https://developer.adobe.com/console). Värdet för `x-api-key` är klient-ID och värdet för `x-gw-ims-org-id` är organisationsnumret.

#### Konfigurera Adobe Developer-konsolen för att generera en åtkomsttoken

Om du vill konfigurera autentiserings-API:er skapar du ett projekt i Adobe Developer Console och lägger till kommunikations-API:er i projektet på Adobe Developer Console. Integreringen genererar API-nyckel, klienthemlighet, nyttolast (JWT):

1. Kontakta Adobe Developer Console-administratören. Be administratören lägga till som utvecklare.
1. Logga in på `https://developer.adobe.com/console/`. Använd ditt utvecklarkonto som administratören har etablerat för att logga in på Adobe Developer Console.
1. Välj organisation i det övre högra hörnet. Kontakta administratören om du inte känner till din organisation.
1. Tryck på **[!UICONTROL Create new project]**. En skärm för att komma igång med ditt nya projekt visas. Tryck på **[!UICONTROL Add API]**. En skärm med en lista över alla API:er som är aktiverade för ditt konto visas.
1. Välj **[!UICONTROL AEM Forms - Communications]** och trycka **[!UICONTROL Next]**. En skärm som konfigurerar API:t visas.
1. Välj **[!UICONTROL OPTION 1 Generate a key pair]** och trycka **[!UICONTROL Generate keypair]**. Konfigurationsfilen skapas och hämtas. Den hämtade konfigurationsfilen innehåller alla programinställningar tillsammans med den enda kopian av din privata nyckel. Adobe spelar inte in din privata nyckel. Spara den hämtade filen på ett säkert sätt. Tryck på **[!UICONTROL Next]**.
1. Välj **[!UICONTROL Integrations - Cloud Service]** och trycka **[!UICONTROL Save configured API]**. Tryck **[!UICONTROL Service Account (JWT)]** om du vill visa API-nyckeln, klienthemligheten och annan information som krävs för att komma åt API:erna. Du anger att du ska använda token för att komma åt API:erna.

#### Generera och använd en åtkomsttoken

Generera en åtkomsttoken genom programmering genom att generera en JSON Web Token (JWT) och byta ut den mot Adobe Identity Management-tjänsten (IMS) för en åtkomsttoken.

Använd följande tangenter, som kallas anspråk, för att konstruera JSON-objekt för JWT:

* `exp`- begärt förfallodatum för åtkomsttoken, uttryckt i antal sekunder sedan 1 januari 1970 GMT. I de flesta fall är detta ett relativt litet värde. I fem minuter från och med nu bör värdet vara 1670923791.
* `iss` - Organisations-ID:t från Adobe Developer Console-projektet i formatet org_ident@AdobeOrg.
* `sub` - ID:t för det tekniska kontot från Adobe Developer Console-integreringen, i följande format: id@techacct.adobe.com.
* `aud` - klient-ID från Adobe Developer Console-integrering som föregås av `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - anges till det literala värdet `true`

Det här JSON-objektet måste sedan vara base64-kodat och signerat med den privata nyckeln för projektet. Slutligen skickas det kodade värdet i brödtexten för en POST-begäran till `https://ims-na1.adobelogin.com/ims/exchange/jwt` tillsammans med klient-ID och klienthemlighet för projektet.

##### Exempel

```JSON
    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache
```

#### Språkstöd för JWT

Även om det går att skapa och utbyta hela JWT-processen i anpassad kod är det vanligare att använda ett bibliotek på högre nivå för att göra det. Ett antal sådana bibliotek visas på [Adobe I/O JWT-dokumentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

### (Endast för API:er för dokumentgenerering) Konfigurera resurser och behörigheter

Följande krävs för att använda synkrona API:er:

* Användare med administratörsbehörighet för Experience Manager
* Överför mallar och annat material till Experience Manager Forms Cloud Service

### (Endast för API:er för dokumentgenerering) Överför mallar och andra resurser till din Experience Manager-instans

En organisation har vanligtvis flera mallar. Till exempel en mall var för kreditkortskontoutdrag, förmånskontoutdrag och ansökningar. Överför alla sådana XDP- och PDF-mallar till din Experience Manager-instans. Så här överför du en mall:

1. Öppna instansen Experience Manager.
1. Gå till Forms > Forms och dokument
1. Klicka på Skapa > Mapp och skapa en mapp. Öppna mappen.
1. Klicka på Skapa > Filöverföring och överför mallarna.

### Anropa ett API

The [API-referensdokumentation](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) innehåller detaljerad information om alla parametrar, autentiseringsmetoder och olika tjänster som tillhandahålls av API:er. API-referensdokumentationen innehåller även API-definitionsfilen i .yaml-format. Du kan hämta .yaml-filen och överföra den till [Postman](https://www.postman.com/) för att kontrollera API:ernas funktioner.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Endast medlemmar i gruppen med formuläranvändare har åtkomst till kommunikationsAPI:er.
