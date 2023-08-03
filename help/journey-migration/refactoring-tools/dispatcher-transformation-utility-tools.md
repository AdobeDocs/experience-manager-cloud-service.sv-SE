---
title: Verktyg för AEM Dispatcher Converter
description: Lär dig hur du konverterar befintliga konfigurationer AEM Dispatcher till konfigurationer AEM as a Cloud Service Dispatcher.
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: f7ffe727ecc7f1331c1c72229a5d7f940070c011
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 18%

---

# AEM Dispatcher Converter {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher Converter"
>abstract="Adobe Experience Manager Dispatcher Converter konverterar befintliga konfigurationer AEM Dispatcher till konfigurationer AEM as a Cloud Service Dispatcher."

Adobe Experience Manager Dispatcher Converter konverterar befintliga konfigurationer AEM Dispatcher till konfigurationer AEM as a Cloud Service Dispatcher.

## Introduktion till Dispatcher {#introduction-dispatcher}

Dispatcher är ett Adobe Experience Manager-verktyg för cachelagring, eller belastningsbalansering, eller båda. AEM:s Dispatcher skyddar också AEM-servern mot angrepp. Därför kan du öka säkerheten för AEM genom att använda Dispatcher med en webbserver i företagsklass.

>[!NOTE]
>Det vanligaste användningsområdet för Dispatcher är att cachelagra svar från en **AEM-publiceringsinstans** för att minska svarstiden och öka säkerheten för den externt adresserade publicerade webbplatsen.

Se [Dispatcher - översikt](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) om du vill veta hur Dispatcher utför cachelagring, returnerar dokument och utför belastningsutjämning.

### Konfiguration och testning av Apache och Dispatcher {#dispatcher-configurations-cloud}

Lär dig att strukturera AEM as a Cloud Service Apache- och Dispatcher-konfigurationer och hur du validerar och kör dem lokalt innan du distribuerar dem till molnmiljöer.

Se [Dispatcher i molnet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html) för mer information.

## AEM Dispatcher Converter {#aem-dispatcher-converter}

Med AEM Dispatcher Converter kan man omfaktorisera befintliga konfigurationer av hanterade tjänster eller Adobe Managed Services Dispatcher till AEM as a Cloud Service kompatibla Dispatcher-konfigurationer.

## Använda AEM Dispatcher Converter   {#using-dispatcher-converter}

* Som Adobe Developer CLI: Adobe rekommenderar vi att du använder AEM Dispatcher Converter via `aio-cli-plugin-aem-cloud-service-migration` (AEM plugin-program för omfaktorisering av as a Cloud Service kod för Adobe Developer CLI).

  Se **[Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** så att du kan lära dig hur du installerar och använder plugin-programmet.

* Som ett fristående verktyg: AEM Dispatcher Converter-verktyget kan också köras som ett fristående verktyg.

  Se **[Git-resurs: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** så att du kan lära dig mer om användningen och felsökningen av det här verktyget.

>[!IMPORTANT]
>AEM Dispatcher Converter utvecklas med NodeJS. Adobe rekommenderar att du har NodeJS 10.0+ installerat.
