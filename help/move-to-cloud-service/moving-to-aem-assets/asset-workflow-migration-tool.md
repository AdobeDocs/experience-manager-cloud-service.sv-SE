---
title: Verktyg för resursarbetsflödesmigrering
description: Verktyg för resursarbetsflödesmigrering
exl-id: 18490295-ead6-4691-8983-a6d4054e4264
source-git-commit: d443ab32e5d2dddded58693483a2bda825ea3048
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 29%

---

# Verktyg för resursarbetsflödesmigrering {#asset-workflow-migration}

Verktyget för resursarbetsflödesmigrering används för att automatiskt migrera arbetsflöden för resursbearbetning från On-premise- eller AMS-driftsättningar till bearbetningsprofiler och OSGi-konfigurationer för användning i AEM Assets as a Cloud Service.

## Introduktion {#introduction}

I det här avsnittet beskrivs resurser och implementeringsinformation för verktyget för resursarbetsflödesmigrering.

Med det här verktyget kan AEM-utvecklare migrera befintliga arbetsflöden för bearbetning av AEM-resurser till AEM as a Cloud Service.

## Arbetsflöden som stöds {#migration-support-for-workflows}

Arbetsflödena har olika nivå av migreringsstöd. Se den här [listan över specifika arbetsflöden](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties). Arbetsflödena kategoriseras i följande kategorier baserat på det stöd som ges. Adobe stöder migrering av arbetsflöden som listas i kategorierna `SUPPORTED`, `REQUIRED` eller `OPTIONAL`. Arbetsflödesstegen som anges i de andra kategorierna stöds inte.

* `SUPPORTED`: Funktioner som stöds i  [!DNL Experience Manager Assets] som Cloud Service.
* `OPTIONAL`: Ytterligare funktioner i  [!DNL Experience Manager Assets] som Cloud Service.
* `REQUIRED`: Ett obligatoriskt steg som läggs till i arbetsflödet.
* `UNNECESSARY`: Funktioner är inte nödvändiga i  [!DNL Experience Manager Assets] som Cloud Service.
* `NUI_OOTB`: Funktioner från  [Asset compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`: Funktioner som tillhandahålls av  [!DNL Dynamic Media] standardanslutningar.
* `NUI_MIGRATED`: Migrerad till en  [bearbetningsprofil för tjänsten](/help/assets/asset-microservices-configure-and-use.md) Asset compute.
* `UNSUPPORTED`: Stöds för närvarande inte i  [!DNL Experience Manager Assets] som Cloud Service.

## Använd verktyget Resursarbetsflödesmigrering {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**: Adobe rekommenderar att du använder verktyget Resursarbetsflödesmigrering via  `aio-cli-plugin-aem-cloud-service-migration` ([!DNL Experience Manager] som ett plugin-program för  [!DNL Cloud Service] kodomfaktorisering för  [!DNL Adobe I/O] CLI). Mer information om hur du installerar och använder plugin-programmet finns i [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction).

* **Fristående verktyg**: Verktyget för migrering av arbetsflöden för resurser kan också köras som ett fristående verktyg. Mer information om hur du installerar och skapar kod från källan finns i [Git-resurs: [!DNL Experience Manager Assets] as a [!DNL Cloud Service] - arbetsflödesmigrering](https://github.com/adobe/aem-cloud-migration).
