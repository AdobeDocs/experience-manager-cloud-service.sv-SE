---
title: Verktyg för AEM Dispatcher Converter
description: Verktyg för AEM Dispatcher Converter
translation-type: tm+mt
source-git-commit: 50d26dbec8281afec07ca56595b4b2a7b915eca9
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 53%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter konverterar befintliga AEM Dispatcher-konfigurationer till AEM som Cloud Service Dispatcher-konfigurationer.

## Introduktion till Dispatcher {#introduction-dispatcher}

Dispatcher är Adobe Experience Managers verktyg för cachelagring och/eller belastningsutjämning. AEM:s Dispatcher skyddar också AEM-servern mot angrepp. Därför kan du öka säkerheten för din AEM-instans genom att använda Dispatcher tillsammans med en företagswebbserver.

>[!NOTE]
>Det vanligaste användningsområdet för Dispatcher är att cachelagra svar från en **AEM-publiceringsinstans** för att minska svarstiden och öka säkerheten för den externt adresserade publicerade webbplatsen.

Läs [Dispatcher-översikt](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) om du vill veta hur Dispatcher utför cachelagring, returnerar dokument och utför belastningsutjämning.

### Konfiguration och testning av Apache och Dispatcher {#dispatcher-configurations-cloud}

Du måste lära dig att strukturera Apache- och Dispatcher-konfigurationer i AEM as a Cloud Service samt att validera och köra det lokalt innan du driftsätter det i molnmiljöer.

Mer information finns i [Dispatcher i molnet](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html).

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter kan omfaktorisera befintliga, lokala eller Adobe Managed Services Dispatcher-konfigurationer så att de AEM som en Cloud Service-kompatibel Dispatcher-konfiguration.

## Använda AEM Dispatcher Converter {#using-dispatcher-converter} 

* Via Adobe I/O CLI: Du bör använda AEM Dispatcher Converter via `aio-cli-plugin-aem-cloud-service-migration` (AEM som ett plugin-program för omfaktorisering av Cloud Service för Adobe I/O CLI).

   Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** för att lära dig hur du installerar och använder plugin-programmet.

* Som fristående verktyg: AEM Dispatcher Converter-verktyget kan också köras som ett fristående verktyg.

   Se **[Git-resurs: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** om du vill veta mer om användning och felsökning för det här verktyget.

>[!IMPORTANT]
>AEM Dispatcher Converter utvecklas med NodeJS. NodeJS 10.0+ bör vara installerat.

