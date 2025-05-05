---
title: Versionsinformation för version 2021.5.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2021.5.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
feature: Release Information
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=sv-SE).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 är 27 maj 2021.
Följande version (2021.6.0) kommer att vara den 28 juni 2021.

## AEM as a Cloud Service Foundation {#foundation}

### Nyheter i AEM as a Cloud Service Foundation {#what-is-new-foundation}

* [Förhandsversion av kanal](/help/release-notes/prerelease.md): Förhandsgranska kommande funktioner under en hel månad innan de publiceras live!

* [API-borttagning](/help/release-notes/deprecated-removed-features.md): det finns en lista över de senaste inaktuella API:erna för AEM as a Cloud Service.

* [AEM as a Cloud Service SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=sv-SE): Uppdatera dina maven-projekt till den senaste versionen, som innehåller en inaktuell Java API-kontroll och andra förbättringar.

## [!DNL Adobe Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* Du kommer snart att kunna verifiera innehåll på ett nytt [förhandsgranskningssteg](/help/sites-cloud/authoring/sites-console/previewing-content.md) för att simulera det slutliga utseendet och utseendet som på Publish-nivån. Detta aktiveras av guiden AEM Sites Managed Publication, som nu låter dig välja ett publiceringsmål mellan Publish eller Preview. Du kommer sedan åt upplevelser på förhandsgranskning via en dedikerad URL. När du har validerat Förhandsgranska kan innehåll publiceras från Författare till Publish som vanligt. Att aktivera förhandsgranskningstjänsten i AEM as a Cloud Service-miljöer kommer gradvis att lanseras under de närmaste veckorna.

## [!DNL Adobe Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nyheter i [!DNL Assets] {#what-is-new-assets}

* Du kan hämta resurser som delas med funktionen Länkdelning. Nedladdningen använder nu en asynkron tjänst som ger snabbare och oavbruten nedladdning, även för mycket stora nedladdningar. Se [hämta resurser](/help/assets/download-assets-from-aem.md#link-share-download).

  ![Hämta inkorgen](/help/assets/assets/download-inbox.png)

### Nya funktioner i prerelease-kanalen {#what-is-new-assets-prerelease}

* Metadata-scheman kan tillämpas direkt på mappegenskaperna.

  ![Lägg till metadataschema från mappegenskaper](/help/assets/assets/metadata-schema-folder-properties.png)

* Med verktyget Massingestor kan du lägga till metadata vid ett massintag.

* En förbättring av användarupplevelsen visar antalet resurser i en mapp. För mer än 1 000 resurser i en mapp visar [!DNL Assets] 1 000+.

  ![Antalet resurser i en mapp visas i gränssnittet](/help/assets/assets/browse-folder-number-of-assets.png)

### Fel som har åtgärdats i [!DNL Assets] {#assets-bugs-fixed}

* När mycket stora filer överförs kraschar [!DNL Experience Manager desktop app]. (CQ-4320942)
* Alternativen i verktygsfältet är olika när samma samling väljs inifrån en mapp och när den väljs från ett sökresultat. (CQ-4321406)

#### Nyheter i Dynamic Media {#what-is-new-dm}

* Med DPR (Smart Imaging DPR) (Device Pixel Ratio) och optimering av nätverksbandbredd kan du leverera bilder av högsta kvalitet effektivt på enheter med högupplösta skärmar och begränsad nätverksbandbredd. Mer information finns i [Vanliga frågor om smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md) och [Bildoptimering med nästa generationens bildformat WebP och AVIF](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4).
* Introducerat stöd för nästa generationens AVIF-bildformat i Dynamic Media-leverans (fmt URL-modifierare).

## [!DNL Adobe Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* **Sammanhangsberoende hjälp**: En sammanhangsberoende hjälp har lagts till för adaptiv formulärredigerare, mallredigerare och temaredigerare för att hjälpa författare att förstå olika funktioner i redigerare.
* **Felmeddelanden i egenskapsläsaren**: Felmeddelanden har lagts till för varje egenskap i webbläsaren Adaptiva Forms-egenskaper. Dessa meddelanden hjälper till att förstå tillåtna värden för ett fält.

### Kommande betafunktion för [!DNL Forms] {#what-is-new-forms-prerelease}

Utdata som en molntjänst: Med Output Service kan du kombinera XDP-mallar och XML-data för att generera utskriftsdokument i olika format. Med tjänsten kan du generera dokument i synkront och asynkront gruppläge. Med Output Service kan du skapa program som gör att du kan:

* Generera slutliga formulärdokument genom att fylla i mallfiler med XML-data.
* Generera utdataformulär i olika format, inklusive icke-interaktiva PDF-utskriftsströmmar.
* Generera PDF från XFA-PDF.

Du kan skriva till formscsbeta@adobe.com och registrera dig för betaprogrammet.

### Fel som har åtgärdats i [!DNL Forms] {#forms-bugs-fixed}

* När du ersätter standardikonen för åtgärdsknapparna med en korallikon i ett steg Tilldela uppgift i AEM Forms Workflows slutar arbetsflödet att fungera och ett undantag loggas. Arbetsflödet fungerar som förväntat när standardikoner används.
* När du ändrar antalet kolumner i layoutlagret öppnar du redigeringslagret och drar några komponenter i en panel visas fyrkantiga blåa rutor i innehållsområdet i den adaptiva formulärredigeraren och redigeraren slutar svara.
* Felmeddelande om ett alternativ för regelredigering som är relaterat till att ange en URL för en adaptiv resurs eller en extern resurs är för lång och inte användarvänlig.


## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.5.0.

### Releasedatum {#release-date-cm-may}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.5.0 är 6 maj 2021.
Nästa version är planerad till 3 juni 2021.

### Nyheter {#what-is-new-may}

* Kvalitetsregeln PackageOverlaps identifierar nu fall där samma paket har distribuerats flera gånger, det vill säga på flera inbäddade platser i samma distribuerade paketuppsättning.

* Databasslutpunkten i det offentliga API:t innehåller nu Git-URL:en.

* Distributionsloggen som laddas ned av en Cloud Manager-användare är mer insiktsfull och innehåller information om fel och lyckade scenarier.

* Intermittenta fel som uppstod när koden skulle skickas till Adobe Git har nu åtgärdats.

* Commerce-tillägg kan nu användas i sandlådeprogram under redigeringsprogrammets arbetsflöde.

* Redigeringsprogrammet har uppdaterats.

* Tabellen Domännamn på sidan Miljöinformation visar upp till 250 domännamn via sidnumrering.

* Lösningen visas på fliken Lösningar i arbetsflödena Lägg till program och Redigera program, även om det bara finns en lösning för programmet.

* Felmeddelandet i byggstegsloggen när bygget inte skapade några distribuerade innehållspaket var oklart.

### Felkorrigeringar {#bug-fixes-cm-may}

* Ibland kan användaren se en grön&quot;aktiv&quot; status bredvid ett IP-Tillåtelselista även när konfigurationen inte har distribuerats.

* I stället för att ta bort &#39;borttagna&#39;-variabler skulle API:t för pipelines-variabler bara markera dem med statusen **DELETED**.

* Vissa problem med saklig kodkvalitet påverkade felaktigt tillförlitlighetsgraderingen.

* Eftersom jokerteckendomäner inte stöds tillåter inte gränssnittet användaren att skicka in en jokerteckendomän.

* När en pipeline-körning startades mellan midnatt och kl. 1:00 UTC var det inte säkert att den artefaktversion som genererades av Cloud Manager var större än den version som skapades föregående dag.

* När projektet med exempelkoden har skapats visas Hantera Git som en länk från hjältekortet på sidan Översikt när sandlådeprogrammet har konfigurerats.

## Verktyget Innehållsöverföring {#content-transfer-tool}

### Releasedatum {#release-date-ctt-latest}

Releasedatum för Content Transfer Tool v1.4.6 är 27 maj 2021.

### Nyheter {#what-is-new-ctt-latest}

* En ny loggningssats har lagts till i snabbstartsloggen, om användaren inte har körningsbehörighet för den körbara Java-filen.

* När en användare tar bort en migreringsuppsättning från CTT-användargränssnittet, där en extrahering utfördes, tas mappen `tmp` som är associerad med den migreringsuppsättningen bort för att spara utrymme.

### Felkorrigeringar {#bug-fixes-ctt-latest}

* När du tar bort en migreringsuppsättning visas ibland ett felmeddelande som inte är användbart i CTT-gränssnittet. Den här har åtgärdats.

* Om användarna hade samma e-postadress på målet och värden men olika användarnamn när användarmappningen kördes, skulle hela inmatningen misslyckas. Den här har åtgärdats. I ett sådant scenario med konflikt hoppas användaren/gruppen över och loggas som en konflikt i loggfilen.

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.4.0 är 11 maj 2021.

### Nyheter {#what-is-new-ctt-may}

* Den här versionen av verktyget Innehållsöverföring skapar textåtergivningar för resurser som migreras till Cloud Service. Textåtergivningar krävs för att ge stöd för fullständig textsökning i kapslade resurser.
* Det maximala antalet migreringsverktyg för innehållsöverföring som en användare kan skapa har ökats från 4 till 10.

### Felkorrigeringar {#bug-fixes-ctt-may}

* Flera felkorrigeringar som rör funktionen för automatisk uppdatering i gränssnittet för verktyget Innehållsöverföring.
* Innehållsöverföringsverktyget med `wipe=true` resulterade i ett felaktigt räknarindex på målet. Den här har åtgärdats.

## Commerce Add-on {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Sidnumreringsstöd för associerat innehåll i produktkonsolens egenskaper

### Felkorrigeringar {#bug-fixes-commerce}

* Miniatyrbilder av resurser visas inte på fliken Resurser i produktegenskaper

* Breadcrumb återställer förhandsvisningsdata i produktkonsolen
