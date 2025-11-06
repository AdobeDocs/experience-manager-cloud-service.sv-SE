---
title: Övertäckningar för Adobe Experience Manager as a Cloud Service
description: AEM as a Cloud Service använder principen för övertäckningar för att du ska kunna utöka och anpassa konsoler och andra funktioner
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Övertäckningar i AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service använder principen för övertäckningar för att du ska kunna utöka och anpassa konsoler och andra funktioner (till exempel för att skapa sidor).

Övertäckning är en term som kan användas i många sammanhang. Om du utökar AEM as a Cloud Service innebär det här en övertäckning att du använder de fördefinierade funktionerna och lägger in egna definitioner över dem för att anpassa standardfunktionerna.

I en standardinstans finns de fördefinierade funktionerna under `/libs` och vi rekommenderar att du definierar övertäckningen (anpassningar) under `/apps` -grenen (använder en [söksökväg](#search-paths) för att matcha resurserna).

* Det beröringskänsliga användargränssnittet använder [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)-relaterade övertäckningar:

   * Metod

      * Rekonstruera lämplig `/libs`-struktur under `/apps`.

        Den här strukturen kräver inte en :1-kopia eftersom [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) används för att korsreferera de ursprungliga definitioner som krävs. Med Sling Resource Merger får du tillgång till och kan sammanfoga resurser med olika mekanismer.

      * Gör ändringar under `/apps`.

   * Fördelar

      * Mer robust för ändringar under `/libs`.
      * Definiera bara om vad som krävs.

>[!CAUTION]
>
>[Samling av resurser](/help/implementing/developing/introduction/sling-resource-merger.md) och de relaterade metoderna kan bara användas med [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Den här regeln innebär att det bara är lämpligt att skapa en övertäckning med en skelettstruktur för det vanliga, beröringsaktiverade användargränssnittet.

Övertäckningar rekommenderas för många ändringar. Du kan till exempel konfigurera dina konsoler eller skapa en markeringskategori i resursläsaren på sidpanelen (används vid utveckling av sidor). De krävs enligt följande:

* **I `/libs`-grenen *ska* inte göra några ändringar**
Alla ändringar du gör kan gå förlorade eftersom den här grenen kan ändras när uppgraderingar tillämpas på din instans.

* De koncentrerar dina ändringar på en plats, vilket gör det enklare för dig att spåra, migrera, säkerhetskopiera eller felsöka ändringarna efter behov.

## Sökvägar {#search-paths}

AEM använder en söksökväg för att hitta en resurs, söker först - som standard - grenen `/apps` och sedan grenen `/libs`. Den här mekanismen innebär att överlägget i `/apps` (och de anpassningar som definierats där) har prioritet.

För övertäckningar är den levererade resursen en sammanställning av resurser och egenskaper som hämtats, beroende på sökvägar som definierats i OSGi-konfigurationen.
