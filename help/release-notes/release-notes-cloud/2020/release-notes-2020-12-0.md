---
title: Versionsinformation om 2020.12.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation om 2020.12.0-utgåvan av [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 är 17 december 2020.
Följande version (2021.1.0) kommer att vara den 28 januari 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[HTTP-API för innehållsfragment](/help/assets/content-fragments/assets-api-content-fragments.md)**: Lägg till/uppdatera och ta bort Content Fragment-varianter med HTTP API.

## [!DNL Adobe Experience Manager Assets] som [!DNL Cloud Service] {#assets}

* Integration med [!DNL Adobe InDesign Server] är nu tillgängligt för [!DNL Experience Manager] som [!DNL Cloud Service]. Den automatiserar processerna [!DNL Adobe InDesign] filer använda [!DNL Adobe InDesign Server] skript och låter användarna använda [!DNL Assets] mallar för användargränssnitt för att skapa broschyrer eller annonser. Endast [!DNL InDesign Server] värd [!DNL Adobe Managed Services] stöds för [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] har förbättrats för att spåra och visa resursreferenser när en resurs används i en fjärranslutning [!DNL Experience Manager Sites] distribution med funktionen för anslutna resurser. En ny [!UICONTROL References] i resursens [!UICONTROL Properties] visas nu lokala referenser och fjärrreferenser för resursen. Med referenserna kan DAM-användare spåra resursanvändning i [!DNL Sites] sidor och i sammansatta resurser i [!DNL Assets]. Se [konfigurera och använda anslutna resurser](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] finns nu tillgängliga via [!DNL Sites] bildbaserade kärnkomponenter. Man kan snabbt konfigurera komponenter så att de använder bildförinställningar, smart beskärning och bildmodifierare när man skapar webbsidor. Se [Core Components 2.13.0 release](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] Med skrivbordsappen kan användare överföra filer och mappar genom att dra filerna från Utforskaren i Windows eller Mac Finder i skrivbordsappens gränssnitt. Se [lägga till resurser med datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Vad är nytt? {#what-is-new-commerce}

* Lanserade CIF Venia Reference Site - 2020.12.01 som innehåller den senaste CIF Core Components version v1.6.0. Se [CIF Venias referenswebbplats](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) för mer information.

* Frisläppta CIF-kärnkomponenter v1.6.0. Se [CIF-kärnkomponenter](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) för mer information.

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i AEM as a Cloud Service 2020.12.0 är 10 december 2020.

### Nyheter i [!DNL Cloud Manager] {#what-is-new-cm}

* Självbetjäningshantering för [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) och [Anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Självbetjäningshantering för [IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* Uppdaterat **Miljö** informationssidan tillåter nu användare att hantera anpassade domännamn och IP-Tillåtelselista i sina miljöer.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Vissa förekomster av fel vid kodskanning utan att ge några resultat åtgärdade.

* Miljökortet visades inte enhetligt **Lägg till** -knappen.

## Verktyg för omstrukturering av kod {#code-refactoring-tools}

### Nyheter i [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Ny version av AIO-CLI-plugin släppt. Den senaste versionen av det här plugin-programmet innehåller felkorrigeringar för AEM Dispatcher Converter och Repository Modernizer och har även stöd för ett nytt verktyg - Index Converter. Se [Enhetlig upplevelse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) om du vill veta mer om det här plugin-programmet.

* Indexkonverteraren är ett verktyg som kan användas för att omvandla en kunds anpassade OAK-indexdefinitioner till AEM as a Cloud Service kompatibla OAK-indexdefinitioner. Se [Indexkonverterare](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) för mer information.

* Ny funktion har lagts till i [Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) som skapar ett separat paket `ui.config` som innehåller alla OSGi-konfigurationer.

### Felkorrigeringar {#crt-bug-fixes}

* Flera felkorrigeringar har gjorts i verktygen AEM Dispatcher Converter och Repository Modernizer. Se [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) och [Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.1.20 är 8 januari 2021.

### Nyheter i [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Användarna kan nu se om deras åtkomsttoken har upphört att gälla genom att hålla markören på statusikonen i användargränssnittet för innehållsöverföringsverktyget (CTT). De får också ett meddelande i användargränssnittet för migreringsuppsättningsinformation om att de inte kan ansluta till sin Cloud Service-instans.

### Felkorrigeringar {#ctt-bug-fixes}

* Status för användargränssnittet i CTT (Content Transfer Tool) för en migreringsuppsättning kvarstod inte och ändrades efter en tids inaktivitet. Den här har åtgärdats.
* Alternativet att visa loggar inaktiverades om loggarna inte var tillgängliga. Detta har åtgärdats och meddelanden har lagts till för att meddela användaren varför loggar saknas.
* Status för användargränssnittet i verktyget Innehållsöverföring visas *MISSLYCKADES* när användaren avbröt ett intag. Detta har korrigerats för visning *STOPPAD* i stället.
