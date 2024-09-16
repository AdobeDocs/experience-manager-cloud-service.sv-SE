---
title: Versionsinformation för version 2020.12.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2020.12.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för [!DNL Experience Manager] as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 är 17 december 2020.
Följande version (2021.1.0) är 28 januari 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[HTTP-API för innehållsfragment](/help/assets/content-fragments/assets-api-content-fragments.md)**: Lägg till/uppdatera och ta bort varianter av innehållsfragment med HTTP-API:t.

## [!DNL Adobe Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

* Integrering med [!DNL Adobe InDesign Server] är nu tillgänglig för [!DNL Experience Manager] som [!DNL Cloud Service]. Den automatiserar bearbetningen av [!DNL Adobe InDesign]-filer med [!DNL Adobe InDesign Server]-skript och gör att användare kan använda [!DNL Assets] -mallar i användargränssnittet för att skapa broschyrer och annonser. Endast [!DNL InDesign Server] som finns hos [!DNL Adobe Managed Services] stöds för [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] har förbättrats för att spåra och visa resursreferenser när en resurs används i en fjärrdistribution av [!DNL Experience Manager Sites] med hjälp av funktionen för anslutna Assets. En ny [!UICONTROL References]-flik på resursens [!UICONTROL Properties]-sida visar nu lokala referenser och fjärrreferenser för resursen. Med referenserna kan DAM-användare spåra resursanvändning på [!DNL Sites] sidor och i sammansatta resurser i [!DNL Assets]. Se [konfigurera och använda anslutna Assets](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media]-funktioner är nu tillgängliga via AEM [!DNL Sites] bildbaserade kärnkomponenter. Man kan snabbt konfigurera komponenter så att de använder bildförinställningar, smart beskärning och bildmodifierare när man skapar webbsidor. Se [Core Components 2.13.0 release](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* Med skrivbordsappen [!DNL Experience Manager] kan användare överföra filer och mappar genom att dra filerna från Utforskaren i Windows eller Mac Finder i skrivbordsappens gränssnitt. Se [lägga till resurser med datorprogrammet](https://experienceleague.adobe.com/en/docs/experience-manager-desktop-app/using/using#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Nyheter {#what-is-new-commerce}

* Lanserade CIF Venia Reference Site - 2020.12.01 som innehåller den senaste CIF Core Components version v1.6.0. Mer information finns i [CIF Venedig-referenswebbplats](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01).

* Frisläppta CIF kärnkomponenter v1.6.0. Mer information finns i [CIF kärnkomponenter](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0).

## Cloud Manager {#cloud-manager}

### Releasedatum {#release-date-cm}

Releasedatum för Cloud Manager i Adobe Experience Manager (AEM) as a Cloud Service 2020.12.0 är 10 december 2020.

### Nyheter i [!DNL Cloud Manager] {#what-is-new-cm}

* Självbetjäningshantering för [SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) och [Introduktion till anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Självbetjäningshantering för [IP Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* På den uppdaterade informationssidan för **Miljö** kan användare nu hantera anpassade domännamn och IP-Tillåtelselista i sina miljöer.

### Felkorrigeringar {#bug-fixes-cloud-manager}

* Vissa fel som inträffar vid kodsökningssteget utan att ge några resultat behandlas.

* Miljökortet visade inte knappen **Lägg till** genomgående.

## Kodomfaktoriseringsverktyg {#code-refactoring-tools}

### Nyheter i [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Ny version av AIO-CLI-plugin släppt. Den senaste versionen av denna plugin innehåller felkorrigeringar för AEM Dispatcher Converter och Repository Modernizer och har även stöd för ett nytt verktyg - Index Converter. Se [Enhetlig upplevelse](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience#benefits) där du kan lära dig mer om det här plugin-programmet.

* Indexkonverteraren är ett verktyg som kan användas för att omvandla en kunds anpassade Oak-indexdefinitioner till AEM as a Cloud Service-kompatibla Oak-indexdefinitioner. Mer information finns i [Indexkonverteraren](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter).

* Ny funktion har lagts till i [Databasmoderering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) som skapar ett separat paket `ui.config` som innehåller alla OSGi-konfigurationer.

### Felkorrigeringar {#crt-bug-fixes}

* Flera felkorrigeringar har gjorts i verktygen AEM Dispatcher Converter och Repository Modernizer. Se [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) och [Databasmoderering](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Releasedatum {#release-date-ctt}

Releasedatum för innehållsöverföringsverktyget v1.1.20 är 8 januari 2021.

### Nyheter i [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Användarna kan nu se om deras åtkomsttoken har upphört att gälla genom att hålla markören på statusikonen i användargränssnittet för innehållsöverföringsverktyget (CTT). De meddelas också i användargränssnittet för migreringsuppsättningsinformation om att de inte kan ansluta till sin Cloud Service-instans.

### Felkorrigeringar {#ctt-bug-fixes}

* Status för användargränssnittet i CTT (Content Transfer Tool) för en migreringsuppsättning kvarstod inte och ändrades efter en tids inaktivitet. Problemet är nu åtgärdat.
* Alternativet att visa loggar inaktiverades om loggarna inte var tillgängliga. Problemet har nu åtgärdats och meddelanden har lagts till för att meddela användarna varför loggar saknas.
* Statusen för användargränssnittet i verktyget Innehållsöverföring visade *MISSLYCKADES* när användaren stoppade ett intag. Problemet har nu åtgärdats så att *STOPPED* visas i stället.
