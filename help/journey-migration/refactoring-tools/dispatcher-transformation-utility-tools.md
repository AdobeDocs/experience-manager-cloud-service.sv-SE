---
title: Verktyg för AEM Dispatcher Converter
description: Lär dig konvertera befintliga konfigurationer på AEM Dispatcher till konfigurationer på AEM as a Cloud Service Dispatcher.
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 13%

---

# AEM Dispatcher Converter {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher Converter"
>abstract="Adobe Experience Manager Dispatcher Converter konverterar befintliga konfigurationer på AEM Dispatcher till konfigurationer på AEM as a Cloud Service Dispatcher."

Adobe Experience Manager Dispatcher Converter konverterar befintliga konfigurationer på AEM Dispatcher till konfigurationer på AEM as a Cloud Service Dispatcher.

## Introduktion till Dispatcher {#introduction-dispatcher}

Dispatcher är Adobe Experience Manager-cachning, eller belastningsutjämningsverktyg, eller båda, verktyg. AEM:s Dispatcher skyddar också AEM-servern mot angrepp. Därför kan du öka säkerheten för AEM genom att använda Dispatcher med en webbserver i företagsklass.

>[!NOTE]
>Det vanligaste användningsområdet för Dispatcher är att cachelagra svar från en **AEM-publiceringsinstans** för att minska svarstiden och öka säkerheten för den externt adresserade publicerade webbplatsen.

Se [Dispatcher-översikt](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) om du vill veta hur Dispatcher utför cachelagring, returnerar dokument och utför belastningsutjämning.

### Konfiguration och testning av Apache och Dispatcher {#dispatcher-configurations-cloud}

Lär dig strukturera konfigurationerna för AEM as a Cloud Service Apache och Dispatcher och hur du validerar och kör dem lokalt innan du distribuerar dem till molnmiljöer.

Mer information finns i [Dispatcher i molnet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html).

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter kan omfaktorisera befintliga Managed Services Dispatcher-konfigurationer på plats eller i Adobe till AEM as a Cloud Service-kompatibla Dispatcher-konfigurationer.

## Använda AEM Dispatcher Converter {#using-dispatcher-converter}

* Som Adobe Developer CLI: Adobe rekommenderar du att du använder AEM Dispatcher Converter via `aio-cli-plugin-aem-cloud-service-migration` (AEM as a Cloud Service code refactoring plugin för Adobe Developer CLI).

  Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** så att du kan lära dig hur du installerar och använder plugin-programmet.

* Som ett fristående verktyg: AEM Dispatcher Converter-verktyget kan också köras som ett fristående verktyg.

  Se **[Git-resurs: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** så att du kan läsa mer om användning och felsökning för det här verktyget.

>[!IMPORTANT]
>AEM Dispatcher Converter utvecklas med NodeJS. Adobe rekommenderar att du har NodeJS 10.0+ installerat.
