---
title: Verktyg för AEM Dispatcher Converter
description: Verktyg för AEM Dispatcher Converter
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 46%

---

# AEM Dispatcher Converter {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher Converter"
>abstract="Adobe Experience Manager Dispatcher Converter konverterar befintliga AEM Dispatcher-konfigurationer till AEM as a Cloud Service Dispatcher-konfigurationer."

Adobe Experience Manager Dispatcher Converter konverterar befintliga AEM Dispatcher-konfigurationer till AEM as a Cloud Service Dispatcher-konfigurationer.

## Introduktion till Dispatcher {#introduction-dispatcher}

Dispatcher är Adobe Experience Managers verktyg för cachelagring och/eller belastningsutjämning. AEM:s Dispatcher skyddar också AEM-servern mot angrepp. Därför kan du öka säkerheten för din AEM-instans genom att använda Dispatcher tillsammans med en företagswebbserver.

>[!NOTE]
>Det vanligaste användningsområdet för Dispatcher är att cachelagra svar från en **AEM-publiceringsinstans** för att minska svarstiden och öka säkerheten för den externt adresserade publicerade webbplatsen.

Läs [Dispatcher-översikt](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) om du vill veta hur Dispatcher utför cachelagring, returnerar dokument och utför belastningsutjämning.

### Konfiguration och testning av Apache och Dispatcher {#dispatcher-configurations-cloud}

Du måste lära dig att strukturera Apache- och Dispatcher-konfigurationer i AEM as a Cloud Service samt att validera och köra det lokalt innan du driftsätter det i molnmiljöer.

Mer information finns i [Dispatcher i molnet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html).

## AEM Dispatcher Converter {#aem-dispatcher-converter}

Med AEM Dispatcher Converter kan man omfaktorisera befintliga konfigurationer av hanterade tjänster eller Adobe Managed Services Dispatcher till AEM as a Cloud Service kompatibla Dispatcher-konfigurationer.

## Använda AEM Dispatcher Converter   {#using-dispatcher-converter}

* Via Adobe I/O CLI: Vi rekommenderar att du använder AEM Dispatcher Converter via `aio-cli-plugin-aem-cloud-service-migration` (AEM plugin-program för omfaktorisering av as a Cloud Service kod för CLI-programmet för Adobe I/O).

   Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** för att lära dig hur du installerar och använder plugin-programmet.

* Som fristående verktyg: AEM Dispatcher Converter-verktyget kan också köras som ett fristående verktyg.

   Se **[Git-resurs: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** om du vill veta mer om användning och felsökning för det här verktyget.

>[!IMPORTANT]
>AEM Dispatcher Converter utvecklas med NodeJS. NodeJS 10.0+ bör vara installerat.
