---
title: Verktyg för resursarbetsflödesmigrering
description: Verktyg för resursarbetsflödesmigrering
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 29%

---

# Verktyg för resursarbetsflödesmigrering {#asset-workflow-migration}

Verktyget för resursarbetsflödesmigrering används för att automatiskt migrera arbetsflöden för resursbearbetning från On-premise- eller AMS-driftsättningar till bearbetningsprofiler och OSGi-konfigurationer för användning i AEM Assets as a Cloud Service.

## Introduktion {#introduction}

I det här avsnittet beskrivs resurser och implementeringsinformation för verktyget för resursarbetsflödesmigrering.

Med det här verktyget kan AEM-utvecklare migrera befintliga arbetsflöden för bearbetning av AEM-resurser till AEM as a Cloud Service.

## Arbetsflöden som stöds {#migration-support-for-workflows}

Arbetsflödena har olika nivå av migreringsstöd. Se det här [lista med specifika arbetsflöden](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties). Arbetsflödena kategoriseras i följande kategorier baserat på det stöd som ges. Adobe har stöd för migrering av de arbetsflöden som är listade i `SUPPORTED`, `REQUIRED`, eller `OPTIONAL` kategorier. Arbetsflödesstegen som anges i de andra kategorierna stöds inte.

* `SUPPORTED`: Funktioner som stöds i [!DNL Experience Manager Assets] as a Cloud Service.
* `OPTIONAL`: Valfri funktionalitet i [!DNL Experience Manager Assets] as a Cloud Service.
* `REQUIRED`: Ett obligatoriskt steg som läggs till i arbetsflödet.
* `UNNECESSARY`: Funktioner är inte nödvändiga i [!DNL Experience Manager Assets] as a Cloud Service.
* `NUI_OOTB`: Funktioner från [Tjänsten Asset compute](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`: Funktioner som anges som standard [!DNL Dynamic Media] kontakter.
* `NUI_MIGRATED`: Migrerad till en [bearbetningsprofil för tjänsten Asset compute](/help/assets/asset-microservices-configure-and-use.md).
* `UNSUPPORTED`: Stöds för närvarande inte i [!DNL Experience Manager Assets] as a Cloud Service.

## Använd verktyget för arbetsflödesmigrering {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**: Adobe rekommenderar att du använder verktyget för arbetsflödesmigrering via `aio-cli-plugin-aem-cloud-service-migration` ([!DNL Experience Manager] som [!DNL Cloud Service] plugin-program för kodomfaktorisering för [!DNL Adobe I/O] CLI). Mer information om hur du installerar och använder plugin-programmet finns i [Git-resurs: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction).

* **Fristående verktyg**: Verktyget för migrering av arbetsflöden för resurser kan också köras som ett fristående verktyg. Mer information om hur du installerar och skapar kod från källan finns i [Git-resurs: [!DNL Experience Manager Assets] som [!DNL Cloud Service] - migrering av arbetsflöden](https://github.com/adobe/aem-cloud-migration).
