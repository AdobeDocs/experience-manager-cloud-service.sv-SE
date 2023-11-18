---
title: Hur använder man Forms as a Cloud Service för att sammanfoga data med XDP- och PDF-mallar eller generera utdata i formaten PCL, ZPL och PostScript?
description: Sammanfoga data automatiskt med XDP- och PDF-mallar eller generera utdata i formaten PCL, ZPL och PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---


# Använd synkron bearbetning {#sync-processing-introduction}

Forms as a Cloud Service - Med API:er för kommunikation kan ni skapa, sammanställa och leverera varumärkesorienterad och personaliserad kommunikation som affärskorrespondenser, dokument, kontoutdrag, kravbrev, förmånsmeddelanden, kravbrev, månadsräkningar och välkomstpaket. Du kan använda API:er för kommunikation för att kombinera en mall (XFA eller PDF) med kunddata för att generera dokument i formaten PDF, PS, PCL, DPL, IPL och ZPL.

Tänk dig ett scenario där du har en eller flera mallar och flera poster med XML-data för varje mall. Du kan använda API:er för kommunikation för att generera ett utskriftsdokument för varje post. <!-- You can also combine the records into a single document. --> Resultatet är ett icke-interaktivt PDF-dokument. Ett icke-interaktivt PDF-dokument tillåter inte att användare anger data i sina fält.

Forms as a Cloud Service - Communications innehåller on demand- och batch-API:er (asynkrona API:er) för schemalagd dokumentgenerering:

* Synkrona API:er är lämpliga för dokumentgenerering on demand, med låg latens och en post. Dessa API:er lämpar sig bättre för användaråtgärdsbaserade användningsfall. Du kan till exempel skapa ett dokument när en användare har fyllt i ett formulär.

* API:er för gruppbearbetning (asynkrona API:er) är lämpliga för schemalagd hög genomströmning vid användning av flera dokumentgenereringar. Dessa API:er genererar dokument gruppvis. Till exempel telefonräkningar, kontoutdrag och förmånsräkningar som genereras varje månad.

## Använd synkrona åtgärder {#batch-operations}

En synkron åtgärd är en process där dokument genereras linjärt. Dessa API:er klassificeras som single-tenant-API:er och multi-tenant-API:er:

### Single-tenant-API:er

* API för dokumentgenerering
* API:er för dokumentbearbetning

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### Autentisera ett single-tenant-API

API-åtgärder för en innehavare har stöd för två typer av autentisering:

* **Grundläggande autentisering**: Grundläggande autentisering är ett enkelt autentiseringsschema som är inbyggt i HTTP-protokollet. Klienten skickar HTTP-begäranden med auktoriseringshuvudet som innehåller ordet Basic följt av ett blanksteg och en base64-kodad sträng med användarnamn:password. Om du till exempel vill auktorisera som administratör/administratör skickar klienten Basic [base64-encoded string username]: [base64-kodat stränglösenord].

* **Tokenbaserad autentisering:** Tokenbaserad autentisering använder en åtkomsttoken (Bearer-autentiseringstoken) för att göra begäranden till Experience Manager as a Cloud Service. AEM Forms as a Cloud Service tillhandahåller API:er för att på ett säkert sätt hämta åtkomsttoken. Så här hämtar och använder du token för att autentisera en begäran:

   1. [Hämta as a Cloud Service autentiseringsuppgifter för Experience Manager från Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Installera as a Cloud Service autentiseringsuppgifter för Experience Manager i din miljö](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Programserver, webbserver eller andra icke-AEM servrar) som är konfigurerade att skicka begäranden till (ringa anrop) molntjänsten.
   1. [Generera en JWT-token och ersätt den med Adobe IMS API:er för en åtkomsttoken](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Kör Experience Manager-API:t med åtkomsttoken som en Bearer-autentiseringstoken.
   1. [Ange lämplig behörighet för den tekniska kontoanvändaren i Experience Manager-miljön](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

  >[!NOTE]
  >
  >Adobe rekommenderar att du använder tokenbaserad autentisering i en produktionsmiljö.

<!-- 

### Authenticate a multi-tenant API

#### Authentication Headers

Every inbound HTTP API call to the multi-tenant API must contain these three headers:


* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

The values which should be sent in the `x-api-key` and `x-gw-ims-org-id` headers are provided in the Credentials details screen in the [Adobe Developer Console](https://developer.adobe.com/console). The value of the `x-api-key` header is the Client ID and the value for the `x-gw-ims-org-id` header is the Organization ID.

#### Configure Adobe Developer console to generate an access token

To set up authentication APIs, create a project in Adobe Developer Console and add Communication APIs to the project on Adobe Developer Console. The integration generates API Key, Client Secret, Payload (JWT):

1. Contact you Adobe Developer Console administrator. Ask the administrator to add as a developer.
1. Log in to `https://developer.adobe.com/console/`. Use your developer account that your administrator has provisioned to log in to Adobe Developer Console.
1. Select your organization from the top-right corner. If you do not know your organization, contact your administrator.
1. Tap **[!UICONTROL Create new project]**. A screen to get started with your new project appears. Tap **[!UICONTROL Add API]**. A screen with list of all the APIs enabled for your account appears.
1. Select **[!UICONTROL AEM Forms - Communications]** and tap **[!UICONTROL Next]**. A screen to configure the API appears.
1. Select **[!UICONTROL OPTION 1 Generate a key pair]** and tap **[!UICONTROL Generate keypair]**. It creates and downloads the configuration file. The downloaded configuration file contains all your app settings, along with the only copy of your private key. Adobe does not record your private key, make sure to securely store the downloaded file. Tap **[!UICONTROL Next]**.
1. Select **[!UICONTROL Integrations - Cloud Service]** and tap **[!UICONTROL Save configured API]**. Tap **[!UICONTROL Service Account (JWT)]** to view the API Key, Client Secret, and other information required to access the APIs. You set to use the token to access the APIs.

#### Programmatically generate and use an access token

To programmatically generate an access token, generate a JSON Web Token (JWT) and exchange it with the Adobe Identity Management Service (IMS) for an access token.

Use the following keys, referred to as claims, to construct JWT JSON object:


* `exp`- the requested expiration of the access token, expressed as several seconds since January 1, 1970 GMT. For most use cases, this is a relatively small value. For example, 5 minutes, for five minutes from now, this value should be 1670923791.
* `iss` - the Organization ID from the Adobe Developer Console project, in the format org_ident@AdobeOrg.
* `sub` - the Technical Account ID from the Adobe Developer Console integration, in the format: id@techacct.adobe.com.
* `aud` - the Client ID from the Adobe Developer Console integration prepended with `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - set to the literal value `true`

This JSON object must be then base64 encoded and signed using the private key for the project. Finally, the encoded value is sent in the body of a POST request to `https://ims-na1.adobelogin.com/ims/exchange/jwt` along with the Client ID and Client Secret for the project.

##### Example

```JSON

    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache

```

#### Language Support for JWT

While it is possible to do the entire JWT generation and exchange process in custom code, it is more common to use a higher-level library to do so. A number of such libraries are listed on the [Adobe I/O JWT Documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

-->

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

>[!MORELIKETHIS]
>
>* [Introduktion till AEM Forms as a Cloud Service Communications](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [AEM Forms as a Cloud Service Architecture for Adaptive Forms and Communication APIs](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Kommunikationsbearbetning - Synkrona API:er](/help/forms/aem-forms-cloud-service-communications.md)
>* [Kommunikationsbearbetning - batch-API:er](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)