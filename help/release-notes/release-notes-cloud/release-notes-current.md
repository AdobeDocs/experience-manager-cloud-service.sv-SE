---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 3452f877960a0067aa4eb1041e58a0b0e64340dd
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---


# Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] som en Cloud Service.

>[!NOTE]
>Härifrån kan du navigera till versionsinformation för tidigare versioner; till exempel för 2020, 2021 och så vidare.

>[!NOTE]
>
>Mer information om dokumentationsuppdateringar som inte är direkt relaterade till en release finns i [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html).

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som Cloud Service 2021.5.0 är 27 maj 2021.
Följande version (2021.6.0) kommer att vara den 24 juni 2021.

## Släpp video {#release-video}

Titta på videon [Versionsöversikt från maj 2021](https://video.tv.adobe.com/v/333602) om du vill se en sammanfattning av de nya funktionerna.

## AEM som Cloud Service Foundation {#foundation}

### Nyheter i AEM som en Cloud Service Foundation {#what-is-new-foundation}

* [Prerelease Channel](/help/release-notes/prerelease.md): Förgranska kommande funktioner under en hel månad innan de går live i produktion!

* [API-borttagning](/help/release-notes/deprecated-apis.md): en lista över de senaste inaktuella API:erna för AEM när en Cloud Service är tillgänglig.

* [AEM som Cloud Service SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html): Uppdatera dina maven-projekt till den senaste versionen, som innehåller en inaktuell Java API-kontroll och andra förbättringar.

## [!DNL Adobe Experience Manager Sites] som  [!DNL Cloud Service] {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* Du kommer snart att kunna verifiera innehåll på en ny [förhandsgranskningsnivå](/help/sites-cloud/authoring/fundamentals/previewing-content.md) för att simulera det slutliga utseendet och känslan som på publiceringsnivån. Detta aktiveras av guiden AEM Sites Managed Publication, som nu låter dig välja ett publiceringsmål mellan Publicera eller Förhandsgranska. Du kommer sedan åt upplevelser på förhandsgranskning via en dedikerad URL. Efter validering i förhandsgranskning kan innehåll publiceras från författare till publicering som vanligt. Om du aktiverar förhandsgranskningstjänsten i AEM som en Cloud Service-miljö kommer den att lanseras gradvis under de kommande veckorna.

## [!DNL Adobe Experience Manager Assets] som  [!DNL Cloud Service] {#assets}

### Nya funktioner i prerelease-kanalen {#what-is-new-assets-prerelease}

* Metadata-scheman kan tillämpas direkt på mappegenskaperna.

   ![Lägg till metadatamatchemat från mappegenskaper](/help/assets/assets/metadata-schema-folder-properties.png)

* Med verktyget Massingestor kan du lägga till metadata vid ett massintag.

* En förbättring av användarupplevelsen visar antalet resurser i en mapp. För mer än 1 000 resurser i en mapp visar [!DNL Assets] 1 000+.

   ![Antalet resurser i en mapp visas i gränssnittet](/help/assets/assets/browse-folder-number-of-assets.png)

### Fel som har korrigerats i [!DNL Assets] {#assets-bugs-fixed}

* När du överför mycket stora filer kraschar [!DNL Experience Manager desktop app]. (CQ-4320942)
* Alternativen i verktygsfältet är olika när samma samling väljs inifrån en mapp och när den väljs från ett sökresultat. (CQ-4321406)

#### Nyheter i [!DNL Dynamic Media] {#what-is-new-dm}

* Med optimering av pixelproportioner för smarta bildbehandlingsenheter (DPR) och nätverksbandbredd kan du leverera bilder av högsta kvalitet effektivt på enheter med högupplösta skärmar och begränsad nätverksbandbredd. Se [Vanliga frågor om smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md).

   >[!NOTE]
   >
   >Tidslinjen i releasen för de ovanstående förbättringarna av Smart Imaging är:
   >
   >* Nordamerika 24 maj 2021 i NA,
      >
      >
   * Europa, Mellanöstern och Afrika 25 juni 2021,
      >
      >
   * Asien-Stillahavsområdet 19 juli 2021.


* Introducerat stöd för nästa generationens AVIF-bildformat i [!DNL Dynamic Media]-leverans (fmt URL-modifierare).

   >[!NOTE]
   >
   >Tidslinjen för releasen för AVIF-stöd är:
   >
   >* Nordamerika 10 maj 2021,
      >
      >
   * Europa, Mellanöstern och Afrika 24 maj 2021,
      >
      >
   * Asien-Stillahavsområdet 24 juni 2021.


## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM som en Cloud Service 2021.5.0.

### Releasedatum {#release-date-cm-may}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.5.0 är 6 maj 2021.
Nästa version är planerad till 10 juni 2021.

### Nyheter {#what-is-new-may}

* Kvalitetsregeln PackageOverlaps identifierar nu fall där samma paket har distribuerats flera gånger, dvs. på flera inbäddade platser, i samma distribuerade paketuppsättning.

* Databasslutpunkten i det offentliga API:t innehåller nu Git-URL:en.

* Distributionsloggen som hämtas av en Cloud Manager-användare blir mer insiktsfull och innehåller nu information om fel och lyckade scenarier.

* Intermittenta fel som uppstod när koden skulle skickas till Adobe Git har nu åtgärdats.

* Tillägget Commerce kan nu användas för sandlådeprogram under arbetsflödet för redigeringsprogram.

* Redigeringsprogrammet har uppdaterats.

* Tabellen Domännamn på sidan Miljöinformation visar upp till 250 domännamn via sidnumrering.

* Lösningen visas på fliken Lösningar i arbetsflödena Lägg till program och Redigera program, även om det bara finns en lösning för programmet.

* Felmeddelandet i byggstegsloggen när bygget inte skapade några distribuerade innehållspaket var oklart.

### Felkorrigeringar {#bug-fixes-cm-may}

* Ibland kan användaren se en grön&quot;aktiv&quot; status bredvid ett IP-Tillåtelselista även när konfigurationen inte har distribuerats.

* I stället för att ta bort &quot;borttagna&quot;-variabler skulle API:t för pipelines-variablerna bara markera dem med statusen **DELETED**.

* Vissa problem med saklig kodkvalitet påverkade felaktigt tillförlitlighetsgraderingen.

* Eftersom jokerteckendomäner inte stöds tillåter inte gränssnittet användaren att skicka in en jokerteckendomän.

* När en pipeline-körning startades mellan midnatt och kl. 1 UTC garanterades inte artefaktversionen som genererades av Cloud Manager att vara större än en version som skapades föregående dag.

* När projektet med exempelkoden har skapats visas Hantera Git som en länk från hjältekortet på sidan Översikt när sandlådeprogrammet har konfigurerats.

## Content Transfer Tool {#content-transfer-tool}

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
