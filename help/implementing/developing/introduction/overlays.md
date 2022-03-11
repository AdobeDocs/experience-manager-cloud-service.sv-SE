---
title: Övertäckningar för Adobe Experience Manager as a Cloud Service
description: AEM as a Cloud Service använder principen om övertäckningar för att du ska kunna utöka och anpassa konsoler och andra funktioner
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 1%

---

# Överlagring i AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service använder principen för övertäckningar för att du ska kunna utöka och anpassa konsoler och andra funktioner (till exempel för att skapa sidor).

Övertäckning är en term som kan användas i många sammanhang. I det här sammanhanget (utöka AEM as a Cloud Service) innebär en övertäckning att du tar de fördefinierade funktionerna och lägger in egna definitioner över dem (för att anpassa standardfunktionerna).

I en standardinstans hålls den fördefinierade funktionen under `/libs` och vi rekommenderar att du definierar övertäckningen (anpassningarna) under `/apps` förgrening (med [söksökväg](#search-paths) för att lösa resurserna).

* Användargränssnittet med pekfunktioner använder [Granit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)-relaterade övertäckningar:

   * Metod

      * Rekonstruera lämplig `/libs` struktur under `/apps`.

         Detta kräver ingen 1:1-kopia eftersom [Samla resurser](/help/implementing/developing/introduction/sling-resource-merger.md) används för att korsreferera till de ursprungliga definitioner som krävs. Med Sling Resource Merger får du tillgång till och kan sammanfoga resurser på olika sätt (differentiering).

      * Gör ändringarna under `/apps`.
   * Fördelar

      * Kraftfullare förändringar under `/libs`.
      * Definiera bara om vad som faktiskt behövs.


>[!CAUTION]
>
>The [Samla resurser](/help/implementing/developing/introduction/sling-resource-merger.md) och de relaterade metoderna kan bara användas med [Granit](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Det innebär att det bara är lämpligt att skapa en övertäckning med en skelettstruktur för det pekaktiverade standardgränssnittet.

Övertäckningar är den rekommenderade metoden för många ändringar, som att konfigurera konsoler eller skapa en markeringskategori för resursläsaren på sidopanelen (används vid utveckling av sidor). De krävs enligt följande:

* Du ***får inte* gör ändringar i `/libs` bankkontor **Alla ändringar du gör kan gå förlorade eftersom den här grenen kan ändras när uppgraderingar tillämpas på din instans.

* De koncentrerar dina ändringar på ett ställe; gör det enklare för dig att spåra, migrera, säkerhetskopiera och/eller felsöka ändringar efter behov.

## Sökvägar {#search-paths}

AEM använder en söksökväg för att hitta en resurs och söker (som standard) först den `/apps` förgrening och sedan `/libs` förgrening. Den här funktionen innebär att överlägget `/apps` (och de anpassningar som definieras där) har prioritet.

För övertäckningar är den levererade resursen en sammanställning av resurser och egenskaper som hämtats, beroende på sökvägar som definierats i OSGi-konfigurationen.
