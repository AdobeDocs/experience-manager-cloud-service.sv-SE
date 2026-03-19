---
title: Konfigurera Assets-väljaren för Universal Editor
description: Lär dig hur du kan konfigurera resursväljaren för användning med den universella redigeraren.
feature: Developing
role: Admin, Developer
source-git-commit: 0ed57393afaf9af3258dacdcb043487f4a098e03
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Konfigurera Assets-väljaren för Universal Editor {#configure-assets-selector}

Lär dig hur du kan konfigurera resursväljaren för användning med den universella redigeraren.

## Ökning {#overview}

Den universella redigeraren använder [resursväljaren](/help/assets/overview-asset-selector.md#using-asset-selector) för att tillåta författare att bläddra bland och välja resurser som ska infogas i deras innehåll.

Resursväljaren kan konfigureras i den universella redigeraren med [-komponentfilter.](/help/implementing/universal-editor/filtering.md) Det här dokumentet beskriver vilka konfigurationsalternativ som är tillgängliga.

>[!NOTE]
>
>När du startar ett Universal Editor-projekt finns det inga filter för resursväljaren. Författare har tillgång till alla resurser som deras användarbehörigheter normalt tillåter.

## Filterdefinition {#filter-definition}

Filterdefinitionen för resursväljaren har en enkel struktur.

```json
[
  {
    "id": "assets-filter",
    "assets": {...}
   }
]
```

## Filteralternativ {#filter-options}

Filtret `assets` kan ha följande alternativ.

* `deliveryTier?`: - Definierar vilket av följande leveransnivåer som ska användas:
   * `dm`: Dynamiska media (rekommenderas) med reserv till `publish` om det behövs
   * `publish`: AEM publiceringsinstans
* `repoNames?`: Sträng - Lista med AEM-databaser som kan användas för att välja bilder.
   * Standard: alla leveransrapporter
* `selectionTier?`: Sträng - AEM skikt för att välja resurser från
   * Standard: `["author", "delivery"]`
* `disableRemote?`: Boolean - Inaktivera stöd för fjärrdatabas
* `preselectedTypes?`: Sträng - förvalda filtyper som ska användas som standardfilter i resursväljaren
* `minMaxDimensions?`: Objekt - Tillhandahåller minimi- och/eller maximidimensioner (i pixlar) som ska användas som standardfilter i resursväljaren
   * `widthMin?`: Nummer - minsta bredd
   * `widthMax?`: Nummer - maximal bredd
   * `heightMin?`: Nummer - minsta höjd
   * `heightMax?`: Nummer - maximal höjd
* `minMaxFileSize?`: Objekt - Ange minsta och/eller största filstorlek (i byte) som ska användas som standardfilter i resursväljaren
   * `min?`: Nummer - minsta filstorlek
   * `max?`: tal - maximal filstorlek
* `customFileTypeFilters?`: Objekt - Anger anpassade filtypsfilter som ska visas i resursväljaren
   * `label`: Sträng - Etikett som ska visas i resursens valda användargränssnitt
   * `value`: Sträng - värde för filtypen som ska filtreras
* `displayFilters?`: Boolean - Används för att inaktivera filtergränssnittet i resursväljaren; true som standard

## Exempel {#example}

Följande exempel innehåller de flesta alternativ för illustrationsändamål.

```json
[
  {
    "id": "assets-filter",
    "assets": {
      "deliveryTier": "dm",
      "repoNames": ["thisRepo", "thatRepo"],
      "selectionTier": ["author", "delivery"],
      "disableRemote": true,
      "preselectedTypes": ["png", "svg", "jpg", "gif"],
      "minMaxDimensions": {
        "widthMin": 640,
        "widthMax": 640,
        "heightMin": 480,
        "heightMax": 480
      },
      "minMaxFileSize": {
        "min": 1024,
        "max": 1024
      }
    }
   }
]
```

## Ytterligare resurser {#additional-resources}

Mer information om resursväljaren finns i dokumentet [Micro-Front Asset Selector](/help/assets/overview-asset-selector.md#using-asset-selector) i resursdokumentationen.
