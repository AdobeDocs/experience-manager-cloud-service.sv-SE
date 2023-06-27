---
title: Övertäckningar för Adobe Experience Manager as a Cloud Service
description: AEM as a Cloud Service använder principen om övertäckningar för att du ska kunna utöka och anpassa konsoler och andra funktioner
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# Överlagring i AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service använder principen för övertäckningar för att du ska kunna utöka och anpassa konsoler och andra funktioner (till exempel för att skapa sidor).

Övertäckning är en term som kan användas i många sammanhang. Om du utökar AEM as a Cloud Service innebär det här ett överlägg att du använder de fördefinierade funktionerna och lägger in egna definitioner över dem för att anpassa standardfunktionerna.

I en standardinstans finns de fördefinierade funktionerna under `/libs` och vi rekommenderar att du definierar övertäckningen (anpassningarna) under `/apps` förgrening (med [söksökväg](#search-paths) för att lösa resurserna).

* Det beröringskänsliga användargränssnittet använder [Granit](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)-relaterade övertäckningar:

   * Metod

      * Rekonstruera lämplig `/libs` struktur under `/apps`.

        Den här strukturen kräver ingen 1:1-kopia eftersom [Samla resurser](/help/implementing/developing/introduction/sling-resource-merger.md) används för att korsreferera till de ursprungliga definitioner som krävs. Med Sling Resource Merger får du tillgång till och kan sammanfoga resurser med olika mekanismer.

      * Under `/apps`, gör ändringar.

   * Fördelar

      * Kraftfullare förändringar under `/libs`.
      * Definiera bara om vad som krävs.

>[!CAUTION]
>
>The [Samla resurser](/help/implementing/developing/introduction/sling-resource-merger.md) och de relaterade metoderna kan bara användas med [Granit](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Den här regeln innebär att det bara är lämpligt att skapa en övertäckning med en skelettstruktur för det vanliga, beröringsaktiverade användargränssnittet.

Övertäckningar rekommenderas för många ändringar. Du kan till exempel konfigurera dina konsoler eller skapa en markeringskategori i resursläsaren på sidpanelen (används vid utveckling av sidor). De krävs enligt följande:

* **I `/libs` gren, *inte* gör ändringar**
Alla ändringar du gör kan gå förlorade eftersom den här grenen kan ändras när uppgraderingar tillämpas på din instans.

* De koncentrerar dina ändringar på en plats, vilket gör det enklare för dig att spåra, migrera, säkerhetskopiera eller felsöka ändringarna efter behov.

## Sökvägar {#search-paths}

AEM använder en söksökväg för att hitta en resurs och söker först - som standard - efter `/apps` förgrening och sedan `/libs` förgrening. Den här funktionen innebär att överlägget `/apps` (och de anpassningar som definieras där) har prioritet.

För övertäckningar är den levererade resursen en sammanställning av resurser och egenskaper som hämtats, beroende på sökvägar som definierats i OSGi-konfigurationen.
