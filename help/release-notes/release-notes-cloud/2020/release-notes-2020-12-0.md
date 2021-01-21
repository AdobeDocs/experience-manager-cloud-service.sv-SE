---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] som en Cloud Service.
translation-type: tm+mt
source-git-commit: 6ea94126d29a470820ee1dc39b239bb10951afac
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

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

Releasedatum för Cloud Manager i AEM som Cloud Service 2020.12.0 är 10 december 2020.

### Nyheter i [!DNL Cloud Manager] {#what-is-new-cm}

* Självbetjäningshantering för [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) och [anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Självbetjäningshantering för [IP Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* **Informationssidan för miljö** tillåter nu användare att hantera anpassade domännamn och IP-Tillåtelselista i sina miljöer.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Vissa förekomster av fel vid kodskanning utan att ge några resultat åtgärdade.

* Miljökortet visade inte **Lägg till**-knapp genomgående.

## Verktyg för omstrukturering av kod {#code-refactoring-tools}

### Nyheter i [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Ny version av AIO-CLI-plugin släppt. Den senaste versionen av det här plugin-programmet innehåller felkorrigeringar för AEM Dispatcher Converter och Repository Modernizer och har även stöd för ett nytt verktyg - Index Converter. Läs [Enhetlig upplevelse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) om du vill veta mer om det här plugin-programmet.

* Indexkonverteraren är ett verktyg som kan användas för att omvandla en kunds anpassade OAK-indexdefinitioner till AEM som en Cloud Service-kompatibel OAK-indexdefinitioner. Mer information finns i [Indexkonverteraren](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter).

* Ny funktion har lagts till i [Databasmodernisering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) som skapar ett separat paket `ui.config` som innehåller alla OSGi-konfigurationer.

### Felkorrigeringar {#crt-bug-fixes}

* Flera felkorrigeringar har gjorts i verktygen AEM Dispatcher Converter och Repository Modernizer. Se [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) och [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).
