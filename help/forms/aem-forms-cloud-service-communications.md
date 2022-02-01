---
title: AEM Forms as a Cloud Service - kommunikation
description: Sammanfoga data automatiskt med XDP- och PDF-mallar eller generera utdata i formaten PCL, ZPL och PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 78cf7d29d6a42f330ba22135c892ce9af5df403f
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# Använd AEM Forms as a Cloud Service kommunikations-API:er - synkron bearbetning {#frequently-asked-questions}

**Kommunikationsfunktionen är i betaversion.**

Med kommunikation kan ni skapa, sammanställa och leverera varumärkesorienterad och personaliserad kommunikation som affärskontakter, dokument, kontoutdrag, kravbrev, förmånsbesked, kravbrev, månatliga räkningar och välkomstpaket. Du kan använda API:er för kommunikation för att kombinera en mall (XFA eller PDF) med kunddata för att generera dokument i formaten PDF, PS, PCL, DPL, IPL och ZPL.

Tänk dig ett scenario där du har en eller flera mallar och flera poster med XML-data för varje mall. Du kan använda API:er för kommunikation för att generera ett utskriftsdokument för varje post. <!-- You can also combine the records into a single document. --> Resultatet är ett icke-interaktivt PDF-dokument. Ett icke-interaktivt PDF-dokument tillåter inte att användare anger data i sina fält.


Kommunikationen tillhandahåller API:er för on demand- och schemalagd dokumentgenerering. Du kan använda synkrona API:er för on demand- och batch-API:er (asynkrona API:er) för schemalagd dokumentgenerering:

* Synkrona API:er är lämpliga för dokumentgenerering on demand, med låg latens och en post. Dessa API:er lämpar sig bättre för användaråtgärdsbaserade användningsfall. Du kan till exempel skapa ett dokument när en användare har fyllt i ett formulär.

* API:er för gruppbearbetning (asynkrona API:er) är lämpliga för schemalagd hög genomströmning vid användning av flera dokumentgenereringar. Dessa API:er genererar dokument gruppvis. Till exempel telefonräkningar, kreditkortsräkningar och förmånsräkningar som genereras varje månad.

## Använd synkrona åtgärder {#batch-operations}

En synkron åtgärd är en process där dokument genereras linjärt. Det stöder två typer av autentisering:

* **Grundläggande autentisering**: Grundläggande autentisering är ett enkelt autentiseringsschema som är inbyggt i HTTP-protokollet. Klienten skickar HTTP-begäranden med auktoriseringshuvudet som innehåller ordet Basic följt av ett blanksteg och en base64-kodad sträng med användarnamn:password. Om du till exempel vill auktorisera som administratör/administratör skickar klienten Basic [base64-kodad stränganvändarnamn]: [base64-kodat stränglösenord].

* **Tokenbaserad autentisering:** Tokenbaserad autentisering använder en åtkomsttoken (Bearer-autentiseringstoken) för att göra begäranden till Experience Manager as a Cloud Service. AEM Forms as a Cloud Service tillhandahåller API:er för att på ett säkert sätt hämta åtkomsttoken. Så här hämtar och använder du token för att autentisera en begäran:

   1. [Hämta as a Cloud Service autentiseringsuppgifter för Experience Manager från Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Installera Experience Manager as a Cloud Service autentiseringsuppgifter i din miljö](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Programserver, webbserver eller andra icke-AEM servrar) som konfigurerats för att skicka begäranden till (ringa anrop) molntjänsten.
   1. [Generera en JWT-token och ersätt den med Adobe IMS API:er för en åtkomsttoken](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Kör Experience Manager-API:t med åtkomsttoken som en Bearer-autentiseringstoken.
   1. [Ange lämplig behörighet för den tekniska kontoanvändaren i Experience Manager-miljön](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe rekommenderar att du använder tokenbaserad autentisering i en produktionsmiljö.

### Krav {#pre-requisites}

Följande krävs för att använda synkrona API:er:

* PDF eller XDP-mallar
* [Data som ska sammanfogas med mallar](#form-data)
* Användare med administratörsbehörighet för Experience Manager
* Överför mallar och annat material till Experience Manager Forms Cloud Service

#### Överför mallar och andra resurser till din Experience Manager-instans

En organisation har vanligtvis flera mallar. Till exempel en mall var för kreditkortskontoutdrag, förmånskontoutdrag och ansökningar. Överför alla sådana XDP- och PDF-mallar till din Experience Manager-instans. Så här överför du en mall:

1. Öppna instansen Experience Manager.
1. Gå till Forms > Forms och dokument
1. Klicka på Skapa > Mapp och skapa en mapp. Öppna mappen.
1. Klicka på Skapa > Filöverföring och överför mallarna.

### Använd synkront API för att generera dokument

Separata API:er är tillgängliga för:

* Skapar ett PDF-dokument från en mall och sammanfogar data till den.
* Skapa ett PostScript- (PS), Printer Command Language (PCL), Zebra Printing Language-dokument (ZPL) från en XDP-fil eller ett PDF-dokument.

The [API-referensdokumentation](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/Communications-Services) innehåller detaljerad information om alla parametrar, autentiseringsmetoder och olika tjänster som tillhandahålls av API:er. API-referensdokumentationen finns också i .yaml-format. Du kan ladda ned .yaml för [synkrona API:er](assets/sync.yaml) och ladda upp det till postman för att kontrollera API:ernas funktionalitet.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>Endast medlemmar i gruppen med formuläranvändare har åtkomst till kommunikationsAPI:er.

