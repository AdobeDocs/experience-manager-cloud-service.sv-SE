---
title: AEM Dispatcher Converter Tool
description: AEM Dispatcher Converter Tool
translation-type: tm+mt
source-git-commit: 66cf4fc7b5a336968dd3f8757cc56a11d6e4843e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter konverterar befintliga AMS Dispatcher-konfigurationer till AEM som en Cloud Service Dispatcher-konfigurationer.

## Introduktion till Dispatcher {#introduction-dispatcher}

Dispatcher är Adobe Experience Manager och/eller belastningsutjämningsverktyg. Med AEM&#39;s Dispatcher kan du även skydda AEM-servern mot attacker. Därför kan du öka säkerheten för din AEM-instans genom att använda Dispatcher tillsammans med en webbserver i företagsklass.

>[!NOTE]
>Det vanligaste användningsområdet för Dispatcher är att cachelagra svar från en **AEM-publiceringsinstans** för att öka svarstiden och säkerheten för den externt adresserade publicerade webbplatsen.

Läs [Dispatcher Overview](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) om du vill veta hur dispatchern utför cachelagring, returnerar dokument och utför belastningsutjämning.

### Konfiguration och testning av Apache och Dispatcher {#dispatcher-configurations-cloud}

Du måste lära dig att strukturera AEM som en Cloud Service-Apache och Dispatcher-konfigurationer samt att validera och köra den lokalt innan du distribuerar den i molnmiljöer.

Mer information finns i [Dispatcher i molnet](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) .

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter är ett verktyg för konvertering av befintliga AMS Dispatcher-konfigurationer till AEM som en Cloud Service Dispatcher-konfigurationer. Det här verktyget är till för AMS-instanser.

Den implementerade konverteraren är **AEMDispatcherConfigConverter** som följer riktlinjerna för omvandling.

Se [Konvertera en AMS till en Cloud Service-Dispatcher-konfiguration](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) för att konvertera en AMS till en Adobe Experience Manager som en Cloud Service-Dispatcher-konfiguration.

## Använda AEM Dispatcher Converter {#using-dispatcher-converter}

I följande avsnitt beskrivs de resurser och den information som krävs för att använda verktyget AEM Dispatcher Converter.

Se **[Git-resurs: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**om du vill veta mer om användning, begränsningar och felsökning för det här verktyget.

>[!IMPORTANT]
>AEM Dispatcher Converter har utvecklats med Python 3.7.3. Vi rekommenderar att du har Python 3.5 eller senare installerat.

## Begränsningar {#limitations}

AEM Dispatcher Converter utgår från att strukturen i den angivna konfigurationsmappen för dispatcher liknar den som beskrivs i Cloud Manager-dispatcherkonfigurationen.


