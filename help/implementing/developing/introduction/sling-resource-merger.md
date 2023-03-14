---
title: Använda Sling Resource Merger i Adobe Experience Manager as a Cloud Service
description: Med Sling Resource Merger får du tillgång till och kan sammanfoga resurser
exl-id: 5b6e5cb5-4c6c-4246-ba67-6b9f752867f5
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 1%

---

# Använda Sling Resource Merger i AEM as a Cloud Service {#using-the-sling-resource-merger-in-aem}

## Syfte {#purpose}

Med Sling Resource Merger får du tillgång till och kan sammanfoga resurser. Den innehåller olika mekanismer (differentiering) för båda:

* **[Övertäckningar](/help/implementing/developing/introduction/overlays.md)** av resurser som använder [sökvägar](/help/implementing/developing/introduction/overlays.md#search-paths).

* **Åsidosättningar** för komponentdialogrutor för det beröringsaktiverade användargränssnittet (`cq:dialog`), använda resurstyphierarkin (med hjälp av egenskapen `sling:resourceSuperType`).

Med Sling Resource Merger sammanfogas överläggnings-/åsidosättningsresurserna och/eller egenskaperna med de ursprungliga resurserna/egenskaperna:

* Innehållet i den anpassade definitionen har en högre prioritet än det ursprungliga (dvs. det *övertäckningar* eller *åsidosättningar* den).

* Vid behov [egenskaper](#properties) som definieras i anpassningen anger du hur innehåll som sammanfogas från originalet ska användas.

>[!CAUTION]
>
>Sling Resource Merger och relaterade metoder kan bara användas med det beröringsaktiverade användargränssnittet (som är det enda användargränssnittet som finns för AEM as a Cloud Service).

### Mål för AEM {#goals-for-aem}

Målet med Sling Resource Merger i AEM är att

* se till att anpassningar inte görs i `/libs`.
* minska strukturen som replikeras från `/libs`.

   När du använder Samling Resource Merger bör du inte kopiera hela strukturen från `/libs` eftersom detta skulle resultera i att för mycket information sparas i anpassningen (vanligen `/apps`). Om du duplicerar information i onödan ökar risken för problem när systemet uppgraderas på något sätt.

>[!CAUTION]
>
>Du ***måste*** ändrar ingenting i `/libs` bana.
>
>Detta beror på innehållet i `/libs` kan skrivas över när som helst när uppgraderingar tillämpas på din instans.
>
>* Övertäckningarna är beroende av [sökvägar](/help/implementing/developing/introduction/overlays.md#search-paths).
>
>* Åsidosättningar är inte beroende av sökvägarna, de använder egenskapen `sling:resourceSuperType` för att skapa anslutningen.
>
>Åsidosättningar definieras ofta under `/apps`, vilket är den bästa metoden inom AEM as a Cloud Service är att definiera anpassningar enligt `/apps`; det beror på att du inte får ändra något under `/libs`.

### Egenskaper {#properties}

Resurskoncentrationen har följande egenskaper:

* `sling:hideProperties` ( `String` eller `String[]`)

   Anger den egenskap, eller lista med egenskaper, som ska döljas.

   Jokertecknet `*` döljer alla.

* `sling:hideResource` ( `Boolean`)

   Anger om resurserna ska vara helt dolda, inklusive dess underordnade.

* `sling:hideChildren` ( `String` eller `String[]`)

   Innehåller den underordnade noden, eller listan med underordnade noder, som ska döljas. Egenskaperna för noden bevaras.

   Jokertecknet `*` döljer alla.

* `sling:orderBefore` ( `String`)

   Innehåller namnet på noden på samma nivå som den aktuella noden ska placeras framför.

Dessa egenskaper påverkar hur motsvarande/ursprungliga resurser/egenskaper (från `/libs`) används av övertäckningen/åsidosättningen (ofta i `/apps`).

### Skapa strukturen {#creating-the-structure}

Om du vill skapa en övertäckning eller åsidosättning måste du återskapa den ursprungliga noden, med motsvarande struktur, under målet (vanligtvis `/apps`). Till exempel:

* Övertäckning

   * Definitionen av navigeringsposten för Sites-konsolen, som visas i järnvägen, definieras på:

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Om du vill täcka över det här skapar du följande nod:

      `/apps/cq/core/content/nav/sites`

      Uppdatera sedan egenskapen `jcr:title` efter behov.

* Åsidosätt

   * Definitionen av den beröringsaktiverade dialogrutan för textkonsolen definieras på:

      `/libs/foundation/components/text/cq:dialog`

   * Om du vill åsidosätta detta skapar du följande nod, till exempel:

      `/apps/the-project/components/text/cq:dialog`

Om du vill skapa någon av dessa behöver du bara återskapa skelettstrukturen. För att förenkla återskapandet av strukturen kan alla mellanliggande noder vara av typen `nt:unstructured` (De behöver inte återspegla den ursprungliga nodtypen. till exempel i `/libs`).

I ovanstående övertäckningsexempel behövs alltså följande noder:

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>När du använder Sling Resource Merger (d.v.s. när du arbetar med standardgränssnittet med pekfunktioner) bör du inte kopiera hela strukturen från `/libs` eftersom det skulle resultera i att för mycket information hålls kvar i `/apps`. Detta kan orsaka problem när systemet uppgraderas på något sätt.

### Användningsexempel {#use-cases}

Dessa tillsammans med standardfunktioner gör att du kan:

* **Lägg till en egenskap**

   Egenskapen finns inte i `/libs` definition, men krävs i `/apps` överlägg/åsidosätt.

   1. Skapa motsvarande nod i `/apps`
   1. Skapa den nya egenskapen på den här noden &quot;

* **Omdefiniera en egenskap (inte automatiskt skapade egenskaper)**

   Egenskapen definieras i `/libs`, men ett nytt värde krävs i `/apps` överlägg/åsidosätt.

   1. Skapa motsvarande nod i `/apps`
   1. Skapa matchande egenskap på den här noden (under / `apps`)

      * Egenskapen får en prioritet baserat på konfigurationen för Sling Resource Resolver.
      * Det går att ändra egenskapstypen.

         Om du använder en annan egenskapstyp än den som används i `/libs`används egenskapstypen som du definierar.
   >[!NOTE]
   >
   >Det går att ändra egenskapstypen.

* **Omdefiniera en egenskap som har skapats automatiskt**

   Som standard skapas automatiskt egenskaper (till exempel `jcr:primaryType`) är inte föremål för en övertäckning/åsidosättning för att säkerställa att den nodtyp som finns under `/libs` respekteras. Om du vill använda en övertäckning/åsidosättning måste du återskapa noden i `/apps`, döljer egenskapen explicit och definierar om den:

   1. Skapa motsvarande nod under `/apps` med önskat `jcr:primaryType`
   1. Skapa egenskapen `sling:hideProperties` på den noden, med värdet inställt på värdet för den automatiskt skapade egenskapen, till exempel `jcr:primaryType`

      Den här egenskapen, definierad under `/apps`, får nu högre prioritet än den som definieras under `/libs`

* **Definiera om en nod och dess underordnade noder**

   Noden och dess underordnade noder definieras i `/libs`, men en ny konfiguration krävs i `/apps` överlägg/åsidosätt.

   1. Kombinera åtgärder från:

      1. Dölj underordnade noder för en nod (behåller nodens egenskaper)
      1. Definiera om egenskapen/egenskaperna

* **Dölj en egenskap**

   Egenskapen definieras i `/libs`, men krävs inte i `/apps` överlägg/åsidosätt.

   1. Skapa motsvarande nod i `/apps`
   1. Skapa en egenskap `sling:hideProperties` av typen `String` eller `String[]`. Använd den här inställningen för att ange vilka egenskaper som ska döljas/ignoreras. Du kan också använda jokertecken. Till exempel:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Dölja en nod och dess underordnade noder**

   Noden och dess underordnade noder definieras i `/libs`, men krävs inte i `/apps` överlägg/åsidosätt.

   1. Skapa motsvarande nod under /apps
   1. Skapa en egenskap `sling:hideResource`

      * typ: `Boolean`
      * value: `true`

* **Dölj underordnade noder för en nod (samtidigt som nodens egenskaper behålls)**

   Noden, dess egenskaper och underordnade noder definieras i `/libs`. Noden och dess egenskaper krävs i `/apps` överlägg/åsidosätt, men vissa eller alla underordnade noder krävs inte i `/apps` överlägg/åsidosätt.

   1. Skapa motsvarande nod under `/apps`
   1. Skapa egenskapen `sling:hideChildren`:

      * typ: `String[]`
      * värde: en lista med underordnade noder (enligt definition i `/libs`) för att dölja/ignorera

      Jokertecknet &amp;ast; kan användas för att dölja/ignorera alla underordnade noder.


* **Ändra ordning på noder**

   Noden och dess jämställda noder definieras i `/libs`. En ny position krävs så att noden återskapas i `/apps` överlägg/åsidosätt, där den nya positionen definieras i referens till lämplig nod på samma nivå i `/libs`.

   * Använd `sling:orderBefore` egenskap:

      1. Skapa motsvarande nod under `/apps`
      1. Skapa egenskapen `sling:orderBefore`:

         Detta anger noden (som i `/libs`) som den aktuella noden ska placeras före:

         * typ: `String`
         * value: `<before-SiblingName>`

### Anropa Sling Resource Merger från koden {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger innehåller två anpassade resursprovidrar - en för övertäckningar och en annan för åsidosättningar. Var och en av dessa kan anropas i koden med hjälp av en monteringspunkt:

>[!NOTE]
>
>När du använder resursen bör du använda rätt monteringspunkt.
>
>Detta garanterar att Sling Resource Merger anropas och att den fullständigt sammanfogade resursen returneras (vilket minskar strukturen som behöver replikeras från) `/libs`).

* Övertäckning:

   * syfte: sammanfoga resurser baserat på sökvägar
   * monteringspunkt: `/mnt/overlay`
   * usage: `mount point + relative path`
   * exempel:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Åsidosätt:

   * syfte: sammanfoga resurser baserat på deras supertyp
   * monteringspunkt: `/mnt/overide`
   * usage: `mount point + absolute path`
   * exempel:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

