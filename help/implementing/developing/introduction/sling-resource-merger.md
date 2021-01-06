---
title: Använda Sling Resource Merger i Adobe Experience Manager som Cloud Service
description: Med Sling Resource Merger får du tillgång till och kan sammanfoga resurser
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 1%

---


# Använda Sling Resource Merger i AEM as a Cloud Service {#using-the-sling-resource-merger-in-aem}

## Syfte {#purpose}

Med Sling Resource Merger får du tillgång till och kan sammanfoga resurser. Den innehåller olika mekanismer (differentiering) för båda:

* **[Översikt](/help/implementing/developing/introduction/overlays.md)** över resurser med  [sökvägar](/help/implementing/developing/introduction/overlays.md#search-paths).

* **Åsidosätter** komponentdialogrutor för det beröringsaktiverade användargränssnittet (`cq:dialog`) med hjälp av resurstyphierarkin (med hjälp av egenskapen  `sling:resourceSuperType`).

Med Sling Resource Merger sammanfogas överläggnings-/åsidosättningsresurserna och/eller egenskaperna med de ursprungliga resurserna/egenskaperna:

* Innehållet i den anpassade definitionen har en högre prioritet än originalets (d.v.s. *övertäckningar* eller *åsidosätter*).

* Om det behövs anger [egenskaper](#properties) som definierats i anpassningen hur innehåll som sammanfogats från originalet ska användas.

<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>Sling Resource Merger och relaterade metoder kan bara användas med det beröringsaktiverade användargränssnittet (som är det enda användargränssnittet som är tillgängligt för AEM som Cloud Service).

### Mål för AEM {#goals-for-aem}

Målet med Sling Resource Merger i AEM är att

* se till att anpassningar inte görs i `/libs`.
* minska strukturen som replikeras från `/libs`.

   När du använder Sling Resource Merger bör du inte kopiera hela strukturen från `/libs` eftersom det skulle resultera i att för mycket information hålls kvar i anpassningen (vanligtvis `/apps`). Om du duplicerar information i onödan ökar risken för problem när systemet uppgraderas på något sätt.

>[!CAUTION]
>
>Du ***får*** inte ändra något i `/libs`-sökvägen.
>
>Detta beror på att innehållet i `/libs` kan skrivas över när uppgraderingar tillämpas på din instans.
>
>* Övertäckningar är beroende av [sökvägar](/help/implementing/developing/introduction/overlays.md#search-paths).
>
>* Åsidosättningar är inte beroende av sökvägarna, de använder egenskapen `sling:resourceSuperType` för att skapa anslutningen.
>
>Åsidosättningar definieras ofta under `/apps`, eftersom det bästa sättet i AEM är att definiera anpassningar under `/apps`. Detta beror på att du inte får ändra något under `/libs`.

### Egenskaper {#properties}

Resurskoncentrationen har följande egenskaper:

* `sling:hideProperties` (  `String` eller  `String[]`)

   Anger den egenskap, eller lista med egenskaper, som ska döljas.

   Jokertecknet `*` döljer alla.

* `sling:hideResource` ( `Boolean`)

   Anger om resurserna ska vara helt dolda, inklusive dess underordnade.

* `sling:hideChildren` (  `String` eller  `String[]`)

   Innehåller den underordnade noden, eller listan med underordnade noder, som ska döljas. Egenskaperna för noden bevaras.

   Jokertecknet `*` döljer alla.

* `sling:orderBefore` (  `String`)

   Innehåller namnet på noden på samma nivå som den aktuella noden ska placeras framför.

Dessa egenskaper påverkar hur motsvarande/ursprungliga resurser/egenskaper (från `/libs`) används av övertäckningen/åsidosättningen (ofta i `/apps`).

### Skapar strukturen {#creating-the-structure}

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

Om du vill skapa någon av dessa behöver du bara återskapa skelettstrukturen. För att förenkla återskapandet av strukturen kan alla mellanliggande noder vara av typen `nt:unstructured` (de behöver inte återspegla den ursprungliga nodtypen). till exempel i `/libs`).

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
>När du använder Sling Resource Merger (d.v.s. när du arbetar med standardgränssnittet med pekfunktioner) bör du inte kopiera hela strukturen från `/libs` eftersom det skulle resultera i att för mycket information hålls i `/apps`. Detta kan orsaka problem när systemet uppgraderas på något sätt.

### Använd fall {#use-cases}

Dessa tillsammans med standardfunktioner gör att du kan:

* **Lägg till en egenskap**

   Egenskapen finns inte i definitionen `/libs`, men krävs i övertäckningen/åsidosättningen `/apps`.

   1. Skapa motsvarande nod i `/apps`
   1. Skapa den nya egenskapen på den här noden &quot;

* **Omdefiniera en egenskap (inte automatiskt skapade egenskaper)**

   Egenskapen definieras i `/libs`, men ett nytt värde krävs i övertäckningen/åsidosättningen `/apps`.

   1. Skapa motsvarande nod i `/apps`
   1. Skapa matchande egenskap på den här noden (under / `apps`)

      * Egenskapen får en prioritet baserat på konfigurationen för Sling Resource Resolver.
      * Det går att ändra egenskapstypen.

         Om du använder en annan egenskapstyp än den som används i `/libs` används den egenskapstyp som du definierar.
   >[!NOTE]
   >
   >Det går att ändra egenskapstypen.

* **Omdefiniera en egenskap som har skapats automatiskt**

   Som standard omfattas inte automatiskt skapade egenskaper (till exempel `jcr:primaryType`) av någon övertäckning/åsidosättning för att säkerställa att den nodtyp som finns under `/libs` respekteras. Om du vill lägga till en övertäckning/åsidosättning måste du återskapa noden i `/apps`, dölja egenskapen explicit och definiera om den:

   1. Skapa motsvarande nod under `/apps` med önskad `jcr:primaryType`
   1. Skapa egenskapen `sling:hideProperties` på den noden med värdet inställt på den automatiskt skapade egenskapen; till exempel `jcr:primaryType`

      Den här egenskapen, som definieras under `/apps`, får nu högre prioritet än den som definieras under `/libs`

* **Definiera om en nod och dess underordnade noder**

   Noden och dess underordnade noder definieras i `/libs`, men en ny konfiguration krävs i övertäckningen/åsidosättningen `/apps`.

   1. Kombinera åtgärder från:

      1. Dölj underordnade noder för en nod (behåller nodens egenskaper)
      1. Definiera om egenskapen/egenskaperna

* **Dölj en egenskap**

   Egenskapen definieras i `/libs`, men krävs inte i övertäckningen/åsidosättningen `/apps`.

   1. Skapa motsvarande nod i `/apps`
   1. Skapa en egenskap `sling:hideProperties` av typen `String` eller `String[]`. Använd den här inställningen för att ange vilka egenskaper som ska döljas/ignoreras. Du kan också använda jokertecken. Till exempel:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Dölja en nod och dess underordnade noder**

   Noden och dess underordnade noder definieras i `/libs`, men krävs inte i övertäckningen/åsidosättningen `/apps`.

   1. Skapa motsvarande nod under /apps
   1. Skapa en egenskap `sling:hideResource`

      * typ: `Boolean`
      * value: `true`

* **Dölj underordnade noder för en nod (samtidigt som nodens egenskaper behålls)**

   Noden, dess egenskaper och underordnade noder definieras i `/libs`. Noden och dess egenskaper krävs i övertäckningen/åsidosättningen `/apps`, men vissa eller alla underordnade noder krävs inte i övertäckningen/åsidosättningen `/apps`.

   1. Skapa motsvarande nod under `/apps`
   1. Skapa egenskapen `sling:hideChildren`:

      * typ: `String[]`
      * värde: en lista över de underordnade noderna (enligt definition i `/libs`) som ska döljas/ignoreras

      Jokertecknets &amp;stämpel;ast; kan användas för att dölja/ignorera alla underordnade noder.


* **Ändra ordning på noder**

   Noden och dess jämställda noder definieras i `/libs`. En ny position krävs så att noden återskapas i övertäckningen/åsidosättningen `/apps`, där den nya positionen definieras i referens till lämplig nod på samma nivå i `/libs`.

   * Använd egenskapen `sling:orderBefore`:

      1. Skapa motsvarande nod under `/apps`
      1. Skapa egenskapen `sling:orderBefore`:

         Detta anger noden (som i `/libs`) som den aktuella noden ska placeras före:

         * typ: `String`
         * värde: `<before-SiblingName>`

### Anropa Sling Resource Merger från koden {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger innehåller två anpassade resursprovidrar - en för övertäckningar och en annan för åsidosättningar. Var och en av dessa kan anropas i koden med hjälp av en monteringspunkt:

>[!NOTE]
>
>När du använder resursen bör du använda rätt monteringspunkt.
>
>Detta garanterar att Sling Resource Merger anropas och att den fullständigt sammanfogade resursen returneras (vilket minskar strukturen som behöver replikeras från `/libs`).

* Övertäckning:

   * syfte: sammanfoga resurser baserat på sökvägar
   * monteringspunkt: `/mnt/overlay`
   * usage: `mount point + relative path`
   * exempel:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Åsidosätt:

   * syfte: sammanfoga resurser baserat på deras supertyp
   * monteringspunkt: `/mnt/overide`
   * användning: `mount point + absolute path`
   * exempel:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

<!--
### Example of Usage {#example-of-usage}

Some examples are covered:

* Overlay:

    * [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
    * [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)

* Override:

    * [Configuring your Page Properties](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
-->
