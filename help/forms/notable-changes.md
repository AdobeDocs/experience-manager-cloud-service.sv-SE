---
title: Vilka är skillnaderna mellan AEM 6.5 Forms och AEM Cloud Service?
description: Jämför AEM 6.5 Forms och AEM Cloud Services och lär dig de viktigaste förändringarna innan du uppgraderar eller migrerar till Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 397e7d4f23202b8ae7419b0ad5436a6a10e2efb8
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 0%

---

# Betydande förändringar för befintliga användare av Adobe Experience Manager 6.5 Forms  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service förändrar de befintliga funktionerna avsevärt jämfört med Adobe Experience Manager Forms On-Premise och [!DNL Adobe-Managed Service] miljöer. De viktigaste skillnaderna anges nedan:

## Inbyggda funktioner i molnet

* Tjänsten har en molnbaserad arkitektur som möjliggör automatisk skalning baserat på belastning, noll driftstopp för uppgraderingar, frekvent och efter lansering av nya funktioner och uppdateringar samt topologier som optimerats för maximal flexibilitet och effektivitet.

* Tjänsten innehåller inga skicka-åtgärder som lagrar data till instanser av Adobe Experience Manager Cloud Service, vilket gör den supersäker. Data som samlas in via formulär skickas direkt till konfigurerade datalager.

* Ett kostnadsfritt CDN (content delivery network) ingår också så att du snabbare kan leverera och återge formulär.


## Uppdateringar av utvecklingsflödet

* Tjänsten tillhandahåller en SDK för att utveckla och testa anpassad kod i en lokal miljö (lokal dator) innan koden distribueras till en Cloud Service. Utvecklare utvecklar och testar anpassade komponenter, teman, arbetsflöden, program, konfigurationer, mallar och mycket mer med SDK på sina lokala datorer. När de har testat den anpassade koden i den lokala utvecklingsmiljön distribuerar de den anpassade koden till en [Forms CS - miljöutveckling eller scenmiljö](/help/implementing/cloud-manager/deploy-code.md) för ytterligare testning innan den marknadsförs till en produktionsmiljö.

* Utvecklarna har samma kod för Cloud Service och lokal utvecklingsmiljö [git-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). En Git-databas, som baseras på AEM Archetype, skapas automatiskt när ett AEM as a Cloud Service program skapas.

  ![automatiskt skapa Git-databas AEM som ett molntjänstprogram](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Utvecklingsflödet för Forms as a Cloud Service är anpassat till AEM Archetype för AEM Cloud Service. Det krävs dock vissa förändringar i Adobe Experience Manager Maven-projekten för att de ska vara kompatibla med AEM Cloud Service. På en hög nivå kräver AEM att innehåll och kod skiljs åt i diskreta delpaket för att se skillnaden mellan muterbart och oföränderligt innehåll. Använd [Verktyget Databasmodernisering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) för att strukturera om befintliga projektpaket genom att separera innehåll och kod i separata paket som är kompatibla med den projektstruktur som har definierats för Adobe Experience Manager as a Cloud Service.

* Innan ni använder era kundpaket med Forms as a Cloud Service måste ni kompilera om den anpassade koden med den senaste versionen av adobe-aemfd-docmanager.

* Använd [AEM Forms as a Cloud Service migreringsverktyg](/help/forms/migrate-to-forms-as-a-cloud-service.md) för att förbereda och migrera dina adaptiva Forms, teman, mallar och molnkonfigurationer från <!-- AEM 6.3 Forms--> AEM 6.4 Forms on OSGi and AEM 6.5 Forms on OSGi to [!DNL AEM] as a Cloud Service. Använd [Git-databasen för ditt program](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) för att importera befintliga adaptiva formulärmallar.

* E-post har som standard bara stöd för HTTP- och HTTP-protokoll. [Kontakta supportteam](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) för att göra det möjligt för portar att skicka e-post och aktivera SMTP-protokoll för din miljö.

## Lokalisering

* URL-konventionen för lokaliserade adaptiva Forms har nu stöd för att ange nationella inställningar i URL:en. Den nya URL-konventionen gör det möjligt att cachelagra lokaliserade formulär på en Dispatcher eller CDN. I en Cloud Service-miljö använder du URL-formatet `http://host:port/content/forms/af/<afName>.<locale>.html` begära en lokaliserad version av ett adaptivt formulär i stället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe rekommenderar att du använder Dispatcher eller CDN-cachning. Det förbättrar återgivningshastigheten i förfyllda formulär.


## Adaptiv Forms

* **Regelredigerare:** AEM Forms as a Cloud Service har en härdad [Regelredigerare](rule-editor.md#visual-rule-editor). Kodredigeraren är inte tillgänglig på Forms as a Cloud Service.

  The [migreringsverktyg](/help/forms/migrate-to-forms-as-a-cloud-service.md) hjälper dig att migrera formulär som har anpassade regler (skapade i kodredigeraren). Verktyget konverterar sådana regler till anpassade funktioner som stöds på Forms as a Cloud Service. Du kan använda de återanvändbara funktionerna med Regelredigeraren för att fortsätta att hämta resultat från regelskript. The `onSubmitError` eller `onSubmitSuccess` funktioner är nu tillgängliga som åtgärder i regelredigeraren.

* **Förifyllningstjänst:** Som standard sammanfogar förifyllningstjänsten data med ett adaptivt formulär på klienten i stället för att sammanfoga data på servern i AEM 6.5 Forms. Funktionen hjälper till att ge snabbare förifyllnad av ett adaptivt formulär. Du kan alltid konfigurera så att kopplingsåtgärden körs på Adobe Experience Manager Forms Server.

* **Skicka-åtgärder:** The **E-post** Skicka-åtgärd innehåller alternativ för att skicka bilagor och bifoga DoR-dokument (Document of Record) med e-post. Du kan använda den istället för **E-posta som PDF** i AEM 6.5 Forms.

* **Tjänsten Automated forms conversion**: Tjänsten tillhandahåller inte någon metamodell för tjänsten Automated forms conversion. Du kan [ladda ned den från Automated forms conversion Service-dokumentationen](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **XSD-baserad, adaptiv Forms:** Du kan använda XDP-mall för att utforma en mall för Dokument för post. Tjänsten stöder inte XFA-baserad Adaptive Forms

* **Komponenter**: Tjänsten stöder inte signering i formulär och inkluderar inte komponenterna Summary och Verify för Adaptive Form.

* **Guidegränssnitt:** Du kan använda [Guidegränssnitt](/help/forms/creating-adaptive-form-core-components.md) för att snabbt konfigurera de vanligaste alternativen och enkelt skapa ett adaptivt formulär.

## Forms Portal

* Tjänsten bevarar inte metadata för utkast och skickade Adaptiv Forms.

## Dokumenttjänster:

Forms as a Cloud Service tillhandahåller RESTful-API:er för dokumentgenerering och dokumentredigering. Du kan använda dessa API:er för att generera eller ändra dokument vid behov eller i grupper, efter behov:

* **Dokumenttjänster: API:er för dokumentgenerering (Output Service)**: I ett enda API-anrop eller en grupp kan du bara använda en mall med flera DATA XML-filer. Det går inte att använda flera mallar med flera datafiler i ett enda API-anrop.

* **API:er för dokumenthantering (Assembler Service)**:

   * De åtgärder som kräver dokumenttjänster eller program är inte tillgängliga. Exempel: Microsoft® Word till PDF, Microsoft® Excel till PDF och HTML till PDF, PostScript (PS) till PDF, XDP till PDF forms stöds inte. Dessa åtgärder kräver Microsoft® Office, Adobe Acrobat, Adobe Distiller respektive Forms Document Service.

   * Konvertera dokument som inte är i PDF till ett PDF-format innan du använder dem med API:er för kommunikationsdokumentmanipulering. Om dina dokument till exempel är i Microsoft® Office-, HTML-, PostScript- (PS) eller XDP-format, konverterar du dessa dokument till PDF innan du använder dem med PDF-dokument. Du kan använda [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) tjänster för sådana konverteringar.

   * Du kan använda en AEM 6.5 Forms-miljö för Digital Signature, Encryption, Reader Extension, Send to printer, Convert PDF och Barcoded Forms.


## Dataintegrering (formulärdatamodell)

* Tjänsten har också stöd för JDBC-anslutning, Microsoft® Dynamics, SalesForce, SOAP-baserade webbtjänster och tjänster som stöder OData.

* Du kan även ansluta AEM användarprofil för att hämta och uppdatera användarinformation.

* Forms datamodell stöder endast HTTP- och HTTPS-slutpunkter för att skicka data. Tjänsten stöder inte ömsesidig SSL för REST-anslutning och x509-certifikatbaserad autentisering för SOAP-datakällor.

* Med Forms as a Cloud Service kan du använda Microsoft® Azure Blob, Microsoft® Sharepoint, Microsoft® OneDrive och tjänster med stöd för vanliga CRUD-åtgärder (Skapa, Läs, Uppdatera och Ta bort) som datalager. Både Open API-specifikationen 2.0 och Open API 3.0 stöds.


## E-signera

* Tjänsten ger en OOTB-integrering med Adobe Sign och stöder DocuSign för e-signaturer.

* Tjänsten stöder även Adobe Sign roller. Du kan konfigurera rollerna i den adaptiva Forms-redigeraren så att företagsanvändare enkelt kan konfigurera signeringsarbetsflöden.


## HTML5 Forms

* Med en AEM 6.5 Forms-miljö kan du:

   * återge dina XDP-baserade formulär som HTML5 Forms. Tjänsten stöder inte HTML5 Forms.

   * hämta in data offline och synkronisera dem nästa gång du är online med [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) app.

## Interaktiv kommunikation

* Du kan använda API:er för kommunikation för att skapa anpassade dokument on-demand eller gruppvis på Forms as a Cloud Service. Du kan använda en AEM 6.5 Forms-miljö för interaktiv kommunikation och användargränssnitt för agenter.

## Se även

* [Migrera från AEM Forms (On-Premise och AMS) till AEM Forms as a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [Lägg till eller skapa Adaptiv Forms på AEM Sites Page](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Skapa en adaptiv form (kärnkomponenter)](/help/forms/creating-adaptive-form-core-components.md)
* [Introduktion till AEM Forms as a Cloud Service](/help/forms/home.md)
* [Konfigurera en lokal utvecklingsmiljö och ett inledande utvecklingsprojekt](/help/forms/setup-local-development-environment.md)


<!--

## Additional Information

* [Introduction to AEM Forms as a Cloud Service](/help/forms/home.md)
* [Set up a local development environment and initial development project](/help/forms/setup-local-development-environment.md)

-->
