---
title: Sidredigeraren, sidopanel
description: Lär dig hur du använder sidopanelen i AEM webbplatsredigeraren för att lägga till komponenter och resurser på sidan.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---


# Sidredigeraren, sidopanel {#side-panel}

Lär dig hur du använder sidopanelen i AEM webbplatsredigeraren för att lägga till komponenter och resurser på sidan.

## Lägen i sidopanelen {#modes}

Sidpanelen är alltid tillgänglig i sidredigeraren genom att trycka på eller klicka på **Växla sidopanel** i verktygsfältet i sidredigeraren.

![Växla sidopanel](assets/editor-side-panel-side-panel-toggle.png)

När du öppnar sidopanelen öppnas den från vänster sida och du kan sedan välja mellan tre viktiga flikar:

* [Komponentwebbläsaren](#components-browser) för att lägga till nytt innehåll på sidan
* [Resursläsaren](#assets-browser) för att lägga till nya resurser på sidan
* [Innehållsträdet](#content-tree) för att bläddra i sidans struktur

## Komponentbläddraren {#components-browser}

[Komponenter](/help/implementing/developing/components/overview.md) är byggstenarna som används för att skapa innehåll med AEM sidredigerare. Du placerar flera komponenter på en sida och konfigurerar deras alternativ för att skapa din innehållssida.

Komponentwebbläsaren visar alla komponenter som är tillgängliga för användning på den aktuella sidan. Dessa kan dras till rätt plats och sedan redigeras för att lägga till ditt innehåll.

Tryck eller klicka på **Komponenter** -fliken i sidopanelen för att komma åt **Komponenter** webbläsare.

![Ikonen för komponentwebbläsaren på sidopanelen](assets/editor-side-panel-components-browser.png)

Utseendet och hanteringen beror på vilken typ av enhet du använder.

### Mobil enhet {#mobile-device-components-browser}

När du öppnar komponentwebbläsaren på en mobil enhet täcker den helt den sida som redigeras.

Om du vill lägga till en komponent på sidan markerar och drar du komponenten och flyttar den åt höger. Komponentwebbläsaren stängs och sidan visas igen där du kan placera komponenten.

![Komponentbläddraren på mobilen](assets/editor-side-panel-mobile-device.png)

>[!NOTE]
>
>En mobil enhet identifieras när bredden är mindre än 1 024 pixlar.

### Skrivbordsenhet {#desktop-device-components-browser}

När du öppnar komponentwebbläsaren på en stationär enhet visas den till vänster i fönstret.

Om du vill lägga till en komponent på sidan klickar du på den önskade komponenten och drar den till önskad plats.

![Komponentwebbläsaren på skrivbordet](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

### Använda komponentwebbläsaren {#using-component-browser}

Komponenter i **Komponenter** webbläsaren representeras av:

* Komponentnamn
* Komponentgrupp (i grått)
* Ikon eller förkortning
   * Standardkomponenternas ikoner är monokroma.
   * Förkortningar är alltid de två första tecknen i komponentnamnet.

I det övre verktygsfältet i **Komponenter** webbläsare:

* Filtrera komponenter efter namn.
* Begränsa visningen till en viss grupp med listrutan.

Om du vill ha en mer detaljerad beskrivning av komponenten kan du markera informationsikonen bredvid komponenten i **Komponenter** webbläsare (om tillgängligt). För **Innehållsfragment**:

![Information om komponentwebbläsare](assets/editor-side-panel-component-description.png)

Mer detaljerad information om vilka komponenter som är tillgängliga finns i [Komponentkonsol.](/help/sites-cloud/authoring/components-console.md)

## Resursläsaren {#assets-browser}

The **Resurser** webbläsaren visar alla [resurser](/help/assets/overview.md) som kan användas på den aktuella sidan.

Tryck eller klicka på **Resurser** på sidopanelen för att bläddra bland resurserna.

![Knappen Resursläsare](assets/editor-side-panel-assets-browser-tab.png)

Oändlig rullning används för att expandera listan med resurser när du rullar.

![Resursläsaren](assets/editor-side-panel-assets-browser.png)

Det faktiska utseendet och hanteringen beror på vilken enhetstyp du använder:

### Mobil enhet {#mobile-device-assets-browser}

När du öppnar resursläsaren på en mobil enhet täcker den helt den sida som redigeras.

Om du vill lägga till en resurs på sidan väljer du och drar den önskade resursen och flyttar den sedan åt höger. Resursläsaren stängs och sidan visas igen, där du kan lägga till resursen i den nödvändiga komponenten.

![Resursläsaren på mobilen](assets/editor-side-panel-assets-browser-mobile.png)

>[!NOTE]
>
>En mobil enhet identifieras när bredden är mindre än 1 024 pixlar.

### Skrivbordsenhet {#desktop-device-assets-browser}

När du öppnar resursläsaren på en stationär enhet öppnas den till vänster i fönstret.

Om du vill lägga till en resurs på sidan markerar du den önskade resursen och drar den till önskad komponent eller plats.

![Resursläsaren på skrivbordet](assets/editor-side-panel-assets-browser-desktop.png)

### Använda Resursläsaren {#using-assets-browser}

Om du vill lägga till en resurs på sidan markerar och drar du den till önskad plats. Detta kan vara:

* En befintlig komponent av lämplig typ.
   * Du kan till exempel dra en resurs av typen bild till en bildkomponent.
* A [platshållare](/help/sites-cloud/authoring/page-editor/edit-content.md#component-placeholder) i styckesystemet för att skapa en komponent av lämplig typ.
   * Du kan till exempel dra en resurs av typen bild till styckesystemet för att skapa en bildkomponent.

>[!NOTE]
>
>Det går att dra och släppa resurser för specifika resurser och komponenttyper. Se [Infoga en komponent med Resursläsaren](/help/sites-cloud/authoring/page-editor/edit-content.md#adding-a-component-from) för mer information.

I det övre verktygsfältet i resursläsaren kan du filtrera resurserna efter:

* Namn
* Bana
* Resurstyp som bilder, videoklipp, dokument, stycken, innehållsfragment och Experience Fragments
* Resursegenskaper som orientering och stil
   * Endast tillgängligt för vissa tillgångstyper

Om du snabbt behöver göra en ändring i en resurs kan du starta [tillgångsredigerare](/help/assets/manage-digital-assets.md) direkt från resursläsaren genom att klicka på redigeringsikonen som visas bredvid resursens namn.

![Knappen Resursredigering](assets/editor-side-panel-asset-edit-button.png)

## Innehållsträd {#content-tree}

The **Innehållsträd** ger en översikt över alla komponenter på sidan i en hierarki så att du snabbt kan se hur sidan är uppbyggd.

>[!NOTE]
>
>Innehållsträdet är inte tillgängligt om du redigerar en sida på en mobil enhet (om webbläsarbredden är mindre än 1024px).

Tryck eller klicka på **Innehållsträd** för att komma åt innehållsträdet.

![Knappen Innehållsträd](assets/editor-side-panel-content-tree-tab.png)

När den är öppen kan du se en trädvyrepresentation av sidan eller mallen, så att det blir lättare att förstå hur innehållet är hierarkiskt strukturerat. På en komplex sida är det också enklare att hoppa mellan sidans komponenter.

![Innehållsträd](assets/editor-side-panel-content-tree.png)

En sida kan enkelt bestå av många av samma typ av komponenter, så att innehållsträdet visar beskrivande text (i grått) efter komponenttypens namn (i svart). Den beskrivande texten kommer från vanliga egenskaper för komponenten, till exempel rubrik eller text.

Komponenttyper visas på användarspråket, medan komponentbeskrivningstexten kommer från sidspråket.

Om du klickar på markören bredvid en komponent kommer den nivån att komprimeras eller utökas.

![Utökning av Content Tree Chevron](assets/editor-side-panel-content-tree-chevron.png)

Om du klickar på komponenten markeras komponenten i sidredigeraren. Vilka åtgärder som är tillgängliga beror på sidstatus. Till exempel:

## En bassida {#basic-page}

Komponenterna på en bassida har de vanliga alternativen.

![Innehållsträdet är markerat](assets/editor-side-panel-content-tree-highlighted.png)

Om komponenten som du klickar på i trädet är redigerbar visas en skiftnyckelsikon till höger om namnet. Om du klickar på den här ikonen öppnas redigeringsdialogrutan för komponenten.

![Redigera innehållsträd](assets/editor-side-panel-content-tree-edit.png)

### En Live-kopia {#live-copy}

En sida som är en del av en [livecopy](/help/sites-cloud/administering/msm/overview.md), där komponenter ärvs från en annan sida, har olika alternativ.

## Associerad innehållsläsare {#associated-content-browser}

Om sidan innehåller innehållsfragment har du även tillgång till [webbläsare för associerat innehåll.](/help/sites-cloud/authoring/fragments/content-fragments.md#using-associated-content)
