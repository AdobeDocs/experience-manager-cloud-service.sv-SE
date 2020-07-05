---
title: Verktyg för AEM Dispatcher Converter
description: Verktyg för AEM Dispatcher Converter
translation-type: ht
source-git-commit: 66cf4fc7b5a336968dd3f8757cc56a11d6e4843e
workflow-type: ht
source-wordcount: '348'
ht-degree: 100%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter konverterar befintliga AMS Dispatcher-konfigurationer till AEM as a Cloud Service Dispatcher-konfigurationer.

## Introduktion till Dispatcher {#introduction-dispatcher}

Dispatcher är Adobe Experience Managers verktyg för cachelagring och/eller belastningsutjämning. AEM:s Dispatcher skyddar också AEM-servern mot angrepp. Därför kan du öka säkerheten för din AEM-instans genom att använda Dispatcher tillsammans med en företagswebbserver.

>[!NOTE]
>Det vanligaste användningsområdet för Dispatcher är att cachelagra svar från en **AEM-publiceringsinstans** för att minska svarstiden och öka säkerheten för den externt adresserade publicerade webbplatsen.

Läs [Dispatcher-översikt](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) om du vill veta hur Dispatcher utför cachelagring, returnerar dokument och utför belastningsutjämning.

### Konfiguration och testning av Apache och Dispatcher {#dispatcher-configurations-cloud}

Du måste lära dig att strukturera AEM as a Cloud Service Apache- och Dispatcher-konfiguration samt att validera och köra den lokalt innan du driftsätter den i molnmiljöer.

Mer information finns i [Dispatcher i molnet](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html).

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter är ett verktyg för konvertering av befintliga AMS Dispatcher-konfigurationer till AEM as a Cloud Service Dispatcher-konfigurationer. Det här verktyget ska användas för AMS-instanser.

Den implementerade konverteraren är **AEMDispatcherConfigConverter** som följer riktlinjerna för omvandling.

Läs [Konvertera en AMS till en Adobe Experience Manager as a Cloud Service Dispatcher-konfiguration](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) för att konvertera en AMS till en Adobe Experience Manager as a Cloud Service Dispatcher-konfiguration.

## Använda AEM Dispatcher Converter {#using-dispatcher-converter} 

I följande avsnitt beskrivs de resurser och den information som krävs för att använda verktyget AEM Dispatcher Converter.

Läs **[Git-resurs: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**om du vill veta mer om användning, begränsningar och felsökning för det här verktyget.

>[!IMPORTANT]
>AEM Dispatcher Converter har utvecklats med Python 3.7.3. Vi rekommenderar att du har Python 3.5 eller senare installerat.

## Begränsningar {#limitations}

AEM Dispatcher Converter fungerar med antagandet att den angivna konfigurationsmappens struktur liknar den som beskrivs i Cloud Manager Dispatchers konfiguration.


