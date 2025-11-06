---
title: Anpassa konsoler
description: Lär dig mer om de olika alternativ som finns i AEM för att anpassa konsolerna i din redigeringsinstans.
exl-id: 832f9a86-07c4-4229-a0dc-8ad50a8195b0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Anpassa konsoler {#customizing-consoles}

AEM innehåller alternativ för att anpassa konsolerna (och [sidredigeringsfunktionen](/help/implementing/developing/extending/page-authoring.md)) för din redigeringsinstans.

## Clientlibs {#clientlibs}

Med Clientlibs kan du utöka standardimplementeringen för att erbjuda nya funktioner, samtidigt som du återanvänder standardfunktioner, objekt och standardmetoder. När du anpassar med klientlib kan du skapa ett eget klientlib under `/apps.`. Det kan till exempel innehålla den kod som krävs för den anpassade komponenten.

Se [Använda bibliotek på klientsidan i AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Övertäckningar {#overlays}

Övertäckningar baseras på noddefinitioner och gör att du kan täcka över standardfunktionerna som finns under `/libs` med din egen anpassade funktion under `/apps`. När du skapar en övertäckning krävs inte en :1-kopia av originalet, eftersom [Sling-resurskonfusion](/help/implementing/developing/introduction/sling-resource-merger.md) tillåter arv.

Övertäckningar kan användas på många sätt för att utöka dina AEM-konsoler. Flera exempel finns i följande avsnitt.

Se även [Övertäckningar för Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

>[!TIP]
>
>Om du är intresserad av alternativ för att anpassa redigeringsgränssnittet läser du [Anpassa sidredigering](/help/implementing/developing/extending/page-authoring.md).

## Anpassa standardvyn för en konsol {#customizing-the-default-view-for-a-console}

Du kan anpassa standardvyn (kolumn, kort, lista) för en konsol:

* Du kan ändra ordningen på vyerna genom att ersätta den önskade posten under:

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * Den första posten är standard.

   * De tillgängliga noderna motsvarar de visningsalternativ som är tillgängliga:

      * `column`
      * `card`
      * `list`

* I en övertäckning för en lista:

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * Definiera följande egenskap:

      * **Namn**: `sling:orderBefore`
      * **Typ**: `String`
      * **Värde**: `column`

### Lägg till en ny åtgärd i verktygsfältet {#add-a-new-action-to-the-toolbar}

Du kan skapa egna komponenter och inkludera motsvarande klientbibliotek för anpassade åtgärder.

* Du kan till exempel skapa åtgärden **Befordra till sociala medier** på:

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * Detta kan sedan anslutas till ett verktygsfältsobjekt på konsolen:

   * `/apps/<yourProject>/admin/ext/launches`

   * I markeringsläge:

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### Begränsa en verktygsfältåtgärd till en viss grupp {#restrict-a-toolbar-action-to-a-specific-group}

Du kan använda ett anpassat återgivningsvillkor om du vill täcka över standardåtgärden och ange särskilda villkor som måste uppfyllas innan den återges.

Du kan till exempel skapa en komponent som styr återgivningsvillkoren enligt en grupp:

* `/apps/myapp/components/renderconditions/group`

Så här använder du åtgärden **Skapa plats** på webbplatskonsolen:

* `/libs/wcm/core/content/sites`

1. Skapa övertäckningen:

   * `/apps/wcm/core/content/sites`

1. Lägg sedan till återgivningsvillkoret för åtgärden:

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

Med hjälp av egenskaper på den här noden kan du definiera `groups` som tillåts utföra den specifika åtgärden, till exempel `administrators`

### Anpassa kolumner i listvyn {#customizing-columns-in-list-view}

Så här anpassar du kolumnerna i listvyn:

1. Lägg över listan med tillgängliga kolumner.

   * På noden:

     `/apps/wcm/core/content/common/availablecolumns`

1. Lägg till dina nya kolumner eller ta bort befintliga.

Om du vill infoga ytterligare data måste du skriva en [PageInfoProvider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) med en `pageInfoProviderType` -egenskap.

>[!NOTE]
>
>Den här funktionen är optimerad för kolumner med textfält. För andra datatyper går det att täcka över `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` i `/apps`.

### Filtreringsresurser {#filtering-resources}

När en konsol används måste användaren ofta välja bland resurser som sidor, komponenter eller resurser. Detta kan vara en lista som författaren måste välja ett objekt från.

För att hålla listan i en rimlig storlek och även relevant för användningsfallet kan ett filter implementeras i form av ett anpassat predikat. Mer information finns i [Anpassa sidredigering](/help/implementing/developing/extending/page-authoring.md#filtering-resources).
