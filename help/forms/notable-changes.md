---
title: Vilka är skillnaderna mellan AEM 6.5 Forms och AEM Cloud Services?
description: Jämför AEM 6.5 Forms och AEM Cloud Services och lär dig de viktigaste ändringarna innan du uppgraderar eller migrerar till Cloud Service.
badgeSaas: label="AEM Forms" type="Positive" tooltip="Gäller AEM Forms)."
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
role: Admin, Developer, User
feature: Adaptive Forms
contentOwner: khsingh
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 0%

---

# Skillnaden mellan AEM 6.5 Forms (AMS och On-Prem) och AEM Forms som molntjänster (AEM CS Forms) {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service medför betydande förändringar av befintliga funktioner jämfört med Adobe Experience Manager Forms On-Premise- och [!DNL Adobe-Managed Service]-miljöer. De viktigaste skillnaderna anges nedan:

## Inbyggda funktioner i molnet

* Tjänsten har en molnbaserad arkitektur som möjliggör automatisk skalning baserat på belastning, noll driftstopp för uppgraderingar, frekvent och efter lansering av nya funktioner och uppdateringar samt topologier som optimerats för maximal flexibilitet och effektivitet.

* Tjänsten innehåller inga skicka-åtgärder som lagrar data till Adobe Experience Manager Cloud Service-instanser, vilket gör den supersäker. Data som samlas in via formulär skickas direkt till konfigurerade datalager.

* Ett kostnadsfritt CDN (content delivery network) ingår också så att du snabbare kan leverera och återge formulär.


## Uppdateringar av utvecklingsflödet

* Tjänsten tillhandahåller en SDK för att utveckla och testa anpassad kod i en lokal miljö (lokal dator) innan koden distribueras till en Cloud Service. Utvecklare utvecklar och testar anpassade komponenter, teman, arbetsflöden, program, konfigurationer, mallar och mycket mer med SDK på sina lokala datorer. När de har testat den anpassade koden i den lokala utvecklingsmiljön distribuerar de den anpassade koden till en [Forms CS-miljö eller scenmiljö](/help/implementing/cloud-manager/deploy-code.md) för vidare testning innan de befordrar den till en produktionsmiljö.

* Utvecklare underhåller kod för Cloud Service och lokal utvecklingsmiljö i en gemensam [Git-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). En Git-databas, som baseras på AEM Archetype, skapas automatiskt när ett AEM as a Cloud Service-program skapas.

  ![skapa Git-databas automatiskt på AEM som ett molntjänstprogram](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Utvecklingsflödet för Forms as a Cloud Service är anpassat till AEM Archetype för AEM Cloud-tjänsten. Det krävs dock vissa ändringar i Adobe Experience Manager Maven-projekt för att de ska vara kompatibla med AEM Cloud-tjänsten. På en hög nivå kräver AEM en separation av innehåll och kod i diskreta delpaket för att respektera delningen mellan muterbart och oföränderligt innehåll. Använd [Databasuppdateringsverktyget](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) för att strukturera om befintliga projektpaket genom att separera innehåll och kod i diskreta paket så att de blir kompatibla med den projektstruktur som har definierats för Adobe Experience Manager as a Cloud Service.

* Innan du använder dina kundpaket med Forms as a Cloud Service måste du kompilera om din anpassade kod med den senaste versionen av adobe-aemfd-docmanager.

* Använd [AEM Forms as a Cloud Service migreringsverktyg](/help/forms/migrate-to-forms-as-a-cloud-service.md) för att förbereda och migrera dina adaptiva Forms-, teman, mallar och molnkonfigurationer från <!-- AEM 6.3 Forms--> AEM 6.4 Forms i OSGi och AEM 6.5 Forms i OSGi till [!DNL AEM] as a Cloud Service. Använd [Git-databasen i programmet](/help/implementing/cloud-manager/managing-code/managing-repositories.md) för att importera befintliga adaptiva formulärmallar.

* E-post har som standard bara stöd för HTTP- och HTTP-protokoll. [Kontakta supportteamet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) om du vill aktivera portar för att skicka e-post och aktivera SMTP-protokoll för din miljö.

## Lokalisering

* URL-konventionen för lokaliserade adaptiva Forms har nu stöd för att ange nationella inställningar i URL:en. Den nya URL-konventionen gör det möjligt att cachelagra lokaliserade formulär på en Dispatcher eller CDN. I en Cloud Service-miljö använder du URL-formatet `http://host:port/content/forms/af/<afName>.<locale>.html` för att begära en lokaliserad version av ett adaptivt formulär i stället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe rekommenderar att du använder Dispatcher- eller CDN-cachning. Det förbättrar återgivningshastigheten i förfyllda formulär.


## Adaptiv Forms

* **Regelredigerare:** AEM Forms as a Cloud Service har en [Regelredigerare](rule-editor.md#visual-rule-editor) som är skarpare. Kodredigeraren är inte tillgänglig i Forms as a Cloud Service.

  Med [migreringsverktyget](/help/forms/migrate-to-forms-as-a-cloud-service.md) kan du migrera formulär som har anpassade regler (skapade i kodredigeraren). Verktyget konverterar sådana regler till anpassade funktioner som stöds i Forms as a Cloud Service. Du kan använda de återanvändbara funktionerna med Regelredigeraren för att fortsätta att hämta resultat från regelskript. Funktionerna `onSubmitError` eller `onSubmitSuccess` är nu tillgängliga som åtgärder i regelredigeraren.

<!--* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server.-->

* **Förifyllningstjänst:** Prefill-tjänsten hämtar data från servern och sammanfogar dem för att förifylla din adaptiva Forms på klientsidan. Den här funktionen hjälper till att ge snabbare ifyllnad av ett adaptivt formulär. Du kan alltid konfigurera [prefill-tjänsten](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/prefill-service-adaptive-forms-article-use.html) så att den kör kopplingsåtgärden på Adobe Experience Manager Forms Server.

* **Skicka-åtgärder:** **E-post**-sändningsåtgärden innehåller alternativ för att skicka bilagor och bifoga DoR-dokument (Document of Record) med e-post. Du kan använda den i stället för åtgärden **Skicka som PDF** som finns i AEM 6.5 Forms.

* **Automatiserad formulärkonverteringstjänst**: Tjänsten tillhandahåller ingen metamodell för automatisk formulärkonverteringstjänst. Du kan [hämta den från dokumentationen för den automatiska formulärkonverteringstjänsten](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **XSD-baserad anpassad, anpassad Forms:** Du kan använda XDP-mall för att utforma en mall för dokument för post. Tjänsten stöder inte XFA-baserad Adaptive Forms

* **Komponenter**: Tjänsten stöder inte signering i formulär och innehåller inte komponenterna Summary och Verify för Adaptiv form.

* **Guidens gränssnitt:** Du kan använda [guidegränssnittet](/help/forms/creating-adaptive-form-core-components.md) för att snabbt konfigurera de gemensamma alternativen och enkelt skapa ett adaptivt formulär.

## Forms Portal

* Tjänsten bevarar inte metadata för utkast och skickade Adaptiv Forms.

## Dokumenttjänster:

Forms as a Cloud Service tillhandahåller RESTful-API:er för dokumentgenerering och dokumentredigering. Du kan använda dessa API:er för att generera eller ändra dokument vid behov eller i grupper, efter behov:

* **Dokumenttjänster: API:er för dokumentgenerering (Output Service)**: I ett enda API-anrop eller en grupp kan du bara använda en mall med flera DATA XML-filer. Det går inte att använda flera mallar med flera datafiler i ett enda API-anrop.

* **API:er för dokumenthantering (Assembler Service)**:

   * De åtgärder som kräver dokumenttjänster eller program är inte tillgängliga. Exempel: Microsoft® Word till PDF, Microsoft® Excel till PDF samt HTML till PDF, PostScript (PS) till PDF, XDP till PDF forms stöds inte. Dessa åtgärder kräver Microsoft® Office, Adobe Acrobat, Adobe Distiller respektive Forms Document Service.

   * Konvertera dokument som är i ett annat format än PDF till ett PDF-format innan du använder dem med API:er för hantering av kommunikationsdokument. Om dina dokument till exempel är i Microsoft® Office-, HTML-, PostScript- (PS) eller XDP-format, konverterar du dessa dokument till PDF-format innan du använder dem med PDF-dokument. Du kan använda tjänsten [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) för sådana konverteringar.

   * Du kan använda en AEM 6.5 Forms-miljö för Digital Signature, Encryption, Reader Extension, Send to printer, Convert PDF och Barcoded Forms.


## Dataintegrering (formulärdatamodell)

* Tjänsten ger även stöd för JDBC-anslutning, Microsoft® Dynamics, Salesforce, SOAP-baserade webbtjänster och tjänster som stöder OData.

* Du kan även ansluta AEM användarprofil för att hämta och uppdatera användarinformation.

* Forms datamodell stöder endast HTTP- och HTTPS-slutpunkter för att skicka data. Tjänsten stöder inte ömsesidig SSL för REST-anslutning och x509-certifikatbaserad autentisering för SOAP-datakällor.

* Forms as a Cloud Service tillåter att Microsoft® Azure Blob, Microsoft® Sharepoint, Microsoft® OneDrive och tjänster som stöder allmänna CRUD-åtgärder (Skapa, Läs, Uppdatera och Ta bort) används som datalager. Både Open API-specifikationen 2.0 och Open API 3.0 stöds.


## E-signera

* Tjänsten erbjuder en OOTB-integrering med Adobe Sign och har stöd för e-signaturer i DocuSign.

* Tjänsten har även stöd för Adobe Sign-roller. Du kan konfigurera rollerna i den adaptiva Forms-redigeraren så att företagsanvändare enkelt kan konfigurera signeringsarbetsflöden.


## HTML5 Forms

* Med en AEM 6.5 Forms-miljö kan du

   * återge dina XDP-baserade formulär som HTML5 Forms. Tjänsten stöder inte HTML5 Forms.

   * hämta in data offline och synkronisera dem nästa gång du återgår online med appen [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) .

## Interaktiv kommunikation

* Du kan använda API:er för kommunikation för att producera personliga dokument on-demand eller gruppvis på Forms as a Cloud Service. Du kan använda en AEM 6.5 Forms-miljö för interaktiv kommunikation och användargränssnitt för agenter.

## Se även

* [Migrera från AEM Forms (On-Premise och AMS) till AEM Forms as a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [Lägg till eller skapa Adaptiv Forms på AEM Sites Page](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Skapa en adaptiv form (kärnkomponenter)](/help/forms/creating-adaptive-form-core-components.md)
* [AEM Forms as a Cloud Service - introduktion](/help/forms/home.md)
* [Konfigurera en lokal utvecklingsmiljö och ett inledande utvecklingsprojekt](/help/forms/setup-local-development-environment.md)


<!--

## Additional Information

* [Introduction to AEM Forms as a Cloud Service](/help/forms/home.md)
* [Set up a local development environment and initial development project](/help/forms/setup-local-development-environment.md)

-->
