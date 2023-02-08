---
title: Senaste underhållsinformation [!DNL Adobe Experience Manager] as a Cloud Service.
description: Senaste underhållsinformation [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 76da86d31e2780c2d22419cb8a338cf37963fad8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 1%

---


# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs de tekniska releasefoterna för den senaste underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 10912 {#release-10912}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 10912, som offentliggjordes den 3 februari 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 9850.

Funktionsaktiveringen för den här underhållsversionen ger dig den fullständiga funktionsuppsättningen. Se [aktuell versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md) för fullständig information.

### Kända fel {#known-issues}

Uppgradera inte om du använder CORS. Vi har identifierat ett problem som påverkar GraphQL innehållsleverans i den här versionen. En ändring i AEM dispatcher-konfiguration runt hur GraphQL beständiga frågor cachelagras kan bryta GraphQL innehållsleverans av beständiga frågor för kunder med en CORS-konfiguration.

### Inbäddade tekniker {#embedded-tech}

| Teknik | Version | Länk |
|---|---|---|
| AEM WCM-kärnkomponenter | Version 2.21.2 | [GitHub](https://github.com/adobe/aem-core-wcm-components) |
