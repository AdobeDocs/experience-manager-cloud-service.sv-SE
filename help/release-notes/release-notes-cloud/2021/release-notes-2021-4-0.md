---
title: Versionsinformation för 2021.4.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för 2021.4.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för den aktuella (senaste) versionen av [!DNL Adobe Experience Manager] as a Cloud Service.

>[!NOTE]
>Härifrån kan du navigera till versionsinformation för tidigare versioner, till exempel för versionerna 2020, 2021 och så vidare.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 är 6 maj 2021.
Följande version (2021.5.0) kommer att vara den 27 maj 2021.

## AEM as a Cloud Service Foundation{#aem-as-a-cloud-service-foundation}

### Nyheter {#what-is-new-foundation}

* [Arbetsflödet Publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow) - En ny arbetsflödesmodell och ett nytt steg ger bättre prestanda vid publicering av djupa innehållshierarkier.

## [!DNL Adobe Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nyheter i [!DNL Sites] {#what-is-new-sites}

* GraphQL Endpoints - det är nu möjligt att aktivera det AEM GraphQL-API:t för enskilda AEM Sites-konfigurationer och att skapa anpassade GraphQL-slutpunkter för dessa konfigurationer med hjälp av ett nytt användargränssnitt för GraphQL Console. Gränssnittet gör det även möjligt att hantera slutpunkter från GraphQL.

* Innehållsmodeller, förbättrad datatyp för datum och tid - det är nu möjligt att konfigurera datumtypen Datum och tid så att endast datum-, tid- eller datum- och tidsinformation kan redigeras.

* Innehållsmodeller, förbättrad datatyp för taggar - det går nu att konfigurera datatypen Tags så att du kan skapa en eller flera taggar.

* Innehållsmodeller, ny datatyp för platshållare på flik - den nya datatypen för platshållare på flikar gör det möjligt att gruppera datatyper i avsnitt som återges under flikar i innehållsfragmentredigeraren.

### Felkorrigeringar i [!DNL Sites] {#bug-fixes-sites}

* Content Fragments - moving content fragments or folders now updates nested references inside the fragment (CQ-4320815)

* GraphQL - beständiga frågor stöder nu användardefinierade slutpunkter som är specifika för AEM Sites-konfigurationer (CQ-4315928)

## [!DNL Adobe Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nyheter i [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager] arkiverar inte enskilda hämtningar av resurser där originalfilen hämtas. Den här förbättringen ger snabbare nedladdning.

* När en resurs hämtas via alternativet för länkdelning kan du nu välja att hämta eller inte hämta återgivningarna. Tidigare hämtades alla resursåtergivningar.

* Administratörer kan konfigurera [!DNL Experience Manager] om du vill ta bort resurskällan efter att ha gjort en massresursinmatning. Se [massmaterialinmatning](/help/assets/add-assets.md#asset-bulk-ingestor).

* När du utför en hälsokontroll för att importera resurser i grupp ger Experience Manager nu fler orsaker till misslyckanden. Se [massmaterialinmatning](/help/assets/add-assets.md#asset-bulk-ingestor).

* När du importerar resurser med bulkimportverktyget har administratörer nu möjlighet att ta bort källfilerna när importen har slutförts. Se [massmaterialinmatning](/help/assets/add-assets.md#asset-bulk-ingestor).

* När du redigerar ett metadataram kan administratörer snabbt och enkelt göra urvalet med ett nytt rotsökvägsväljarfält, vilket minskar konfigurationstiden.

* När du redigerar ett metadataschema läggs en datatyp till som ger ett friformstextområde i metadataredigeraren. Användare kan använda det här textområdet för att ange frihandstext som metadata för en resurs. Se [metadatamatchredigerare](/help/assets/metadata-schemas.md).

* Metadata för många resurser kan importeras gruppvis med hjälp av en CSV-fil och kan exporteras till en CSV-fil. Standarddatumformatet är nu `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. Användare kan använda ett annat format genom att uppdatera kolumnrubriken. Lägg till exempel `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` som kolumnrubrik i CSV-filen i stället för ordet `Date`.

* När du bläddrar bland resurser i kolumnvyn visas en visuell indikator med statusen Godkänd eller Avvisad för varje resurs.

* När du bläddrar bland resurser i kolumnvyn visas en visuell indikator för förfallna resurser.

### Felkorrigeringar i [!DNL Assets] {#bug-fixes-assets}

* När du försöker flytta flera resurser eller mappar loggas ett fel i konsolen och flyttåtgärden slutförs inte. Flyttåtgärden misslyckas om titeln inte kan uppdateras. (CQ-4322080)

* Ett metadatafält kan döljas baserat på en regel som gör att metadata inte är obligatoriska när ett fördefinierat villkor är uppfyllt. Sådana dolda metadatafält visas dock som obligatoriska fält. (CQ-4321285)

* Import av massmetadata misslyckas på grund av felaktigt datumformat. (CQ-4319014)

* När du har valt att uppdatera metadata på egenskapssidan tar det lång tid för gränssnittet att svara när det finns många alternativ i schemat. (CQ-4318538)

* När du uppdaterar och sparar metadatavärde i ett enkelradigt textfält tas värdena i listrutan bort, även om redigeringar är inaktiverade på listrutemenyn. (CQ-4317077)

* Du kan använda ellips som en anteckning för att granska resurser. När en liten ellips används överlappar ellipsen numret på anteckningen i utskriftsversionen. (CQ-4316792)

* Alternativet Snabb publicering visas inte när en resurs har valts från sökresultatet efter att ha sökt efter den. (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nyheter i [!DNL Forms] {#what-is-new-forms}

* **Använd autentiseringsmetoden för myndighets-ID i Adobe Sign-aktiverad Adaptive Forms**

  Adobe Sign Government ID-process drivs av avancerade maskininlärningsalgoritmer och ger företag över hela världen möjlighet att säkra en högkvalitativ autentisering av mottagarens identitet. Nu kan du använda autentiseringsmetoden för myndighets-ID i Adobe Sign-aktiverade Adaptive Forms.

  Myndighets-ID är en autentiseringsmetod för premiumidentitet som instruerar mottagaren att [ladda upp bilden av ett foto på ett foto av ett foto av ett foto som utfärdats av en myndighet (körkort, nationellt ID, pass)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)och utvärderar sedan dokumentet för att säkerställa att det är autentiskt.

* **Stöd för att använda signeringsfunktionen i formulär för asynkrona inskickade formulär med adaptiv formatering**

  Nu kan du använda signeringsfunktionen i formulär för asynkrona, anpassningsbara formulärinskickade formulär. Du kan även bädda in ett anpassat formulär i en [!DNL Experience Manager Sites] och använda signeringsfunktionen i formulär för att skicka formulär med adaptiv form.

* **Stöd för att använda en variabel för att ange en bifogad fil när ett adaptivt formulär fylls i i förväg för steget Tilldela uppgift**

  När du fyller i ett adaptivt formulär i förväg för steget Tilldela uppgift kan du nu använda en dokumenttypsvariabel för att välja en bifogad inmatning för det adaptiva formuläret.

* **Stöd för att använda det literala alternativet för att ange ett värde för en JSON-typvariabel**

  Du kan använda det literala alternativet för att ange ett värde för en JSON-typvariabel i det angivna variabelsteget i ett AEM arbetsflöde. Med alternativet literal kan du ange en JSON i form av en sträng.

* **Använd lokal utvecklingsmiljö för att skapa en dokumentfil (DoR)**

  Du kan använda en XDP-fil som en dokumentmall på Cloud Service och AEM Forms as a Cloud Service SDK (lokal utvecklingsmiljö). Tidigare var stödet begränsat till endast Cloud Service.

### Felkorrigeringar i [!DNL Forms] {#bug-fixes-forms}

* När ett anpassat formulär som inte har konfigurerats för att generera ett postdokument skickas till ett AEM arbetsflöde som har konfigurerats för att generera ett postdokument, visas inget felmeddelande och uppgiften kan inte skickas.

### Andra uppdateringar {#misc-2021-04-0-forms}

* För att göra det enklare att identifiera innehåll genererar tjänsten nu dynamiska miniatyrbilder för XDP-, Dynamic PDF- och Schema-filer.
* Lägg till möjligheten att flytta en PDF-fil till en mapp som är placerad i AEM Forms användargränssnitt.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Stöd för kategori-UID - Detta frigör e-handelsintegreringar från tredje part för system som använder strängar för kategori-ID

* AEM för PWA Studio inkl. exempelintegrering

* Ny CIF navigeringskärnkomponent som utökar WCM-navigeringskärnkomponenten

* Visuell indikator för mellanlagrade katalogdata i AEM

* Commerce-slutpunkten kan nu konfigureras via användargränssnittet i Cloud Manager

### Felkorrigeringar {#bug-fixes-commerce}

* Rotkategorifältet visades inte under fliken E-handel i sidegenskaperna för kategorisidor

## Cloud Manager {#cloud-manager}

I det här avsnittet beskrivs versionsinformationen för Cloud Manager i AEM as a Cloud Service 2021.4.0.

### Releasedatum {#release-date-cm-april}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2021.4.0 är 8 april 2021.
Nästa version är planerad till 6 maj 2021.

### Nyheter {#what-is-new-april}

* Gränssnittsuppdateringar i arbetsflödena för Lägg till och redigera program gör dem mer intuitiva.

* En användare med nödvändig behörighet kan nu skicka slutpunkten för e-handeln via användargränssnittet.

* Miljövariabler kan nu omfatta en viss tjänst, antingen författare eller publicerad. AEM version krävs `2021.03.5104.20210328T185548Z` eller senare.

* The **Hantera Git** knappen visas på pipelines-kortet även när inga rörledningar har konfigurerats.

* Den version av AEM projekttyp som används av Cloud Manager har uppdaterats till version 27.

* Projekt i Adobe I/O Developer Console som har skapats i Cloud Manager kan inte längre redigeras eller tas bort oavsiktligt.

* När en användare lägger till en ny miljö informeras de om att när en miljö har skapats kan den inte flyttas till en annan region.

* Miljövariabler kan nu omfatta en viss tjänst, antingen författare eller publicerad. Kräver AEM version 2021.03.5104.20210328T185548Z eller senare.

* Felmeddelandet när en pipeline startades när en miljö togs bort har klargjorts.

* OSGi-paket som tillhandahålls av Eclipse-projekt är nu undantagna från regeln `CQBP-84--dependencies`.

### Felkorrigeringar {#bug-fixes-cm-april}

* När du redigerar Experience Audit-sidan för en pipeline ska du ange en indatasökväg som börjar med ett snedstreck `( / )` kommer inte längre att resultera i att steget fastnar i väntande status.

* När en ny produktionspipeline skapas granskades inte standardstartsidan om användaren inte lägger till någon åsidosättning av innehållsgranskning.

* Problem med `CloudServiceIncompatibleWorkflowProcess` hade fel allvarlighetsgrad i CSV-filen för den hämtningsbara utgåvan.

* The `Runmode` kontrollen genererade falskt positiva värden på noder som inte finns i mappen.

## Best Practices Analyzer {#best-practices-analyzer}

### Releasedatum {#release-date-bpa}

Releasedatum för Best Practices Analyzer v2.1.12 är 12 april 2021.

### Felkorrigeringar {#bug-fixes-bpa-april}

* Dubblettrader sågs i den rapporterade BPA-filen. Den här har åtgärdats.
* BPA-gränssnittet i AEM version 6.4.2 genererade ett JS-fel som inaktiverade knappen Generera rapport. Detta har åtgärdats
