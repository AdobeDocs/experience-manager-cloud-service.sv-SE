---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
translation-type: tm+mt
source-git-commit: 76da904f4fc5a96e6892242c42bae5d05eea2e16
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---


# Versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] som en Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som Cloud Service 2020.12.0 är 17 december 2020.
Följande version (2021.1.0) kommer att vara den 28 januari 2021.

## [!DNL Adobe Experience Manager Sites] som en Cloud Service  {#sites}

* **[HTTP-API](/help/assets/content-fragments/assets-api-content-fragments.md)** för innehållsfragment: Lägg till/uppdatera och ta bort Content Fragment-varianter med HTTP API.

## [!DNL Adobe Experience Manager Assets] som  [!DNL Cloud Service] {#assets}

* Integrering med [!DNL Adobe InDesign Server] är nu tillgängligt för [!DNL Experience Manager] som [!DNL Cloud Service]. Det automatiserar bearbetningen av [!DNL Adobe InDesign]-filer med [!DNL Adobe InDesign Server]-skript och gör att användare kan använda [!DNL Assets]-mallar för att skapa broschyrer och annonser. Endast [!DNL InDesign Server] som är värd för [!DNL Adobe Managed Services] stöds för [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] har förbättrats för att spåra och visa resursreferenser när en resurs används i en fjärrdistribution  [!DNL Experience Manager Sites] med funktionen för anslutna resurser. En ny [!UICONTROL References]-flik på resursens [!UICONTROL Properties]-sida visar nu lokala referenser och fjärrreferenser för resursen. Med referenserna kan DAM-användare spåra resursanvändning på [!DNL Sites]-sidor och i sammansatta resurser i [!DNL Assets]. Se [konfigurera och använda anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] funktioner är nu tillgängliga via  [!DNL Sites] bildbaserade kärnkomponenter. Man kan snabbt konfigurera komponenter så att de använder bildförinställningar, smart beskärning och bildmodifierare när man skapar webbsidor. Se [Core Components 2.13.0 release](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] Med skrivbordsappen kan användare överföra filer och mappar genom att dra filerna från Utforskaren i Windows eller Mac Finder i skrivbordsappens gränssnitt. Se [lägga till resurser med skrivbordsappen](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce som Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Lanserade CIF Venia Reference Site - 2020.12.01 som innehåller den senaste CIF Core Components version v1.6.0. Mer information finns i [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01).

* Frisläppta CIF-kärnkomponenter v1.6.0. Mer information finns i [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0).

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM som Cloud Service 2021.1.0 är 14 januari 2021.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Resursinstansen Production kan vid olika tillfällen visa status för varumärkesportalen på **miljöinformationssidan** som *Väntande* utan att tillåta användaren att vidta några åtgärder.

* När en avaktivering från molnhanteraren utlöstes visades ibland ett felmeddelande även när avviloläget startades.

* Sällsynta fall av fel som uppstått när miljön skapades eller togs bort har åtgärdats.

## Verktyg för omstrukturering av kod {#code-refactoring-tools}

### Nyheter i [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Ny version av AIO-CLI-plugin släppt. Den senaste versionen av det här plugin-programmet innehåller felkorrigeringar för AEM Dispatcher Converter och Repository Modernizer och har även stöd för ett nytt verktyg - Index Converter. Läs [Enhetlig upplevelse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) om du vill veta mer om det här plugin-programmet.

* Indexkonverteraren är ett verktyg som kan användas för att omvandla en kunds anpassade OAK-indexdefinitioner till AEM som en Cloud Service-kompatibel OAK-indexdefinitioner. Mer information finns i [Indexkonverteraren](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter).

* Ny funktion har lagts till i [Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) som skapar ett separat paket `ui.config` som innehåller alla OSGi-konfigurationer.

### Felkorrigeringar {#crt-bug-fixes}

* Flera felkorrigeringar har gjorts i verktygen AEM Dispatcher Converter och Repository Modernizer. Se [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) och [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## Verktyg för övergång till molnet{#code-transition-tools}

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.2.2 är 1 februari 2021.

### Nyheter i [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Ny funktion och nytt användargränssnitt har lagts till i verktyget Innehållsöverföring - verktyget för användarmappning. Den här funktionen mappar automatiskt befintliga användare och grupper till deras Adobe Identity Management-system-ID som en del av innehållsmigreringsaktiviteten. Mer information finns i [Använda verktyget för användarmappning](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html).
* Verktyget Innehållsöverföring migrerar nu alla grupper och användare som det hänvisas till i migreringsuppsättningen, inklusive underordnade.
* Användarna kan välja vissa sökvägar under `/etc` när de skapar migreringsuppsättningar.
