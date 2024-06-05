---
title: Verktyg för resursarbetsflödesmigrering
description: Verktyg för resursarbetsflödesmigrering
exl-id: a95caf5e-e6b2-463f-bebd-b791104fd25c
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 30%

---

# Verktyg för resursarbetsflödesmigrering {#asset-workflow-migration}

Verktyget för resursarbetsflödesmigrering används för att automatiskt migrera arbetsflöden för resursbearbetning från On-premise- eller AMS-driftsättningar till bearbetningsprofiler och OSGi-konfigurationer för användning i AEM Assets as a Cloud Service.

## Introduktion {#introduction}

I det här avsnittet beskrivs resurser och implementeringsinformation för verktyget för resursarbetsflödesmigrering.

Med det här verktyget kan AEM-utvecklare migrera befintliga arbetsflöden för bearbetning av AEM-resurser till AEM as a Cloud Service.

## Arbetsflöden som stöds {#migration-support-for-workflows}

Arbetsflödena har olika nivå av migreringsstöd. Se det här [lista med specifika arbetsflöden](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties). Arbetsflödena kategoriseras i följande kategorier baserat på det stöd som ges. Adobe har stöd för migrering av de arbetsflöden som finns i `SUPPORTED`, `REQUIRED`, eller `OPTIONAL` kategorier. Arbetsflödesstegen som anges i de andra kategorierna stöds inte.

* `SUPPORTED`: Funktioner som stöds i [!DNL Experience Manager Assets] as a Cloud Service.
* `OPTIONAL`: Valfri funktionalitet i [!DNL Experience Manager Assets] as a Cloud Service.
* `REQUIRED`: Ett obligatoriskt steg som läggs till i arbetsflödet.
* `UNNECESSARY`: Funktionalitet är inte nödvändig i [!DNL Experience Manager Assets] as a Cloud Service.
* `NUI_OOTB`: Funktioner från [Tjänsten Asset compute](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`: Funktioner som anges som standard [!DNL Dynamic Media] kontakter.
* `NUI_MIGRATED`: Flyttad till en [bearbetningsprofil för tjänsten Asset compute](/help/assets/asset-microservices-configure-and-use.md).
* `UNSUPPORTED`: Stöds för närvarande inte i [!DNL Experience Manager Assets] as a Cloud Service.

## Använd verktyget för resursarbetsflödesmigrering {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**: Adobe rekommenderar att du använder verktyget Resursarbetsflödesmigrering via `aio-cli-plugin-aem-cloud-service-migration` ([!DNL Experience Manager] som [!DNL Cloud Service] plugin-program för kodomfaktorisering för [!DNL Adobe I/O] CLI). Mer information om hur du installerar och använder plugin-programmet finns i [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction).

* **Fristående verktyg**: Verktyget Resursarbetsflödesmigrering kan också köras som ett fristående verktyg. Mer information om hur du installerar och skapar kod från källan finns i [Git-resurs: [!DNL Experience Manager Assets] som [!DNL Cloud Service] - migrering av arbetsflöden](https://github.com/adobe/aem-cloud-migration).
