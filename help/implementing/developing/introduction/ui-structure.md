---
title: Struktur för AEM
description: Det AEM användargränssnittet har flera bakomliggande principer och består av flera nyckelelement
exl-id: ac211716-d699-4fdb-a286-a0a1122c86c5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 0%

---

# Struktur för AEM {#structure-of-the-aem-ui}

Det AEM användargränssnittet har flera bakomliggande principer och består av flera nyckelelement:

## Konsoler {#consoles}

### Grundläggande layout och storleksändring {#basic-layout-and-resizing}

Gränssnittet fungerar både för mobila och stationära enheter, men i stället för att skapa två format använder AEM ett format som fungerar för alla skärmar och enheter.

Alla moduler använder samma grundläggande layout:

![AEM Sites-konsol](assets/ui-sites-console.png)

Layouten följer en responsiv designstil och passar sig till storleken på enheten, fönstret eller båda, som du använder.

När upplösningen till exempel är lägre än 1 024 pixlar (som på en mobil enhet) justeras visningen därefter:

![Mobilvyn i webbplatskonsolen](assets/ui-sites-mobile.png)

### Sidhuvudsfält {#header-bar}

![AEM rubrikfält](assets/ui-header-bar.png)

Rubrikraden visar globala element som:

* Logotypen och den specifika produkt/lösning som du för närvarande använder. För AEM utgör det här elementet även en länk till den globala navigeringen
* Sök
* Ikon för att komma åt hjälpresurserna
* Ikon för att komma åt andra lösningar
* En indikator på - och åtkomst till - alla varningar och inkorgsobjekt som väntar på dig
* Användarikonen tillsammans med en länk till din profilhantering

### Verktygsfält {#toolbar}

Verktygsfältet är sammanhangsberoende för din plats och de ytverktyg som är relevanta för att styra vyn eller resurserna på sidan nedan. Verktygsfältet är produktspecifikt, men det finns vissa gemensamma element.

I verktygsfältet visas de åtgärder som är tillgängliga för tillfället:

![AEM Sites-verktygsfält](assets/ui-sites-toolbar.png)

Även beroende på om en resurs är markerad:

![AEM Sites-verktygsfältet har valts](assets/ui-sites-toolbar-selected.png)

### Vänster linje {#left-rail}

Den vänstra listen kan öppnas/döljas efter behov för att visa:

* **Endast innehåll**
* **Innehållsträd**
* **Tidslinje**
* **Referenser**
* **Filter**

Standardvärdet är **Endast innehåll** (dold räl).

![Vänster linje](assets/ui-left-rail.png)

## Sidredigering {#page-authoring}

När du skapar sidor är de strukturella områdena följande.

### Innehållsram {#content-frame}

Sidinnehållet återges i innehållsramen. Innehållsramen är oberoende av redigeraren för att säkerställa att det inte finns några konflikter på grund av CSS eller JavaScript.

Innehållsramen finns till höger i fönstret, under verktygsfältet.

![Innehållsram](assets/ui-content-frame.png)

### Redigeringsram {#editor-frame}

Redigeringsramen aktiverar redigeringsfunktionerna.

Redigeringsramen är en behållare (abstrakt) för alla sidredigeringselement. Den ligger ovanpå innehållsramen och innehåller:

* Det övre verktygsfältet
* Sidpanelen
* Alla övertäckningar
* Andra sidredigeringselement, till exempel komponentens verktygsfält

![Redigeringsram](assets/ui-editor-frame.png)

### Side Panel {#side-panel}

Innehåller tre standardflikar. På flikarna **Assets** och **Komponenter** kan du markera sådana element och dra dem från panelen och släppa dem på sidan. På fliken **Innehållsträd** kan du inspektera hierarkin med innehåll på sidan.

Sidpanelen är dold som standard. När du väljer det här alternativet visas det antingen på den vänstra sidan eller när fönsterbredden är mindre än 1 024 pixlar, flyttas det över för att täcka hela fönstret som t.ex. på en mobil enhet.

![Sidpanelen](assets/ui-side-panel.png)

### Side Panel - Assets {#side-panel-assets}

På fliken Assets kan du välja bland flera olika resurser. Du kan också filtrera efter en viss term eller markera en grupp.

![Fliken Assets](assets/ui-side-panel-assets.png)

### Side Panel - Resursgrupper {#side-panel-asset-groups}

På fliken Assets finns en listruta där du kan välja en specifik resursgrupp.

![Resursgrupper](assets/ui-side-panel-asset-groups.png)

### Side Panel - Components {#side-panel-components}

På fliken Komponenter kan du välja bland komponenterna. Du kan också filtrera efter en viss term eller markera en grupp.

![Fliken Komponenter](assets/ui-side-panel-components.png)

### Panelen Sida - Innehållsträd {#side-panel-content-tree}

På fliken Innehållsträd kan du visa hierarkin med innehåll på sidan. Om du klickar på en post på fliken flyttas den till och markerar objektet på sidan i redigeraren.

![Innehållsträdet](assets/ui-side-panel-content-tree.png)

### Övertäckningar {#overlays}

Överlappar innehållsramen och används av [lagren](#layer) för att realisera mekanismerna för hur du kan interagera genomskinligt med komponenterna och deras innehåll.

Övertäckningarna finns i redigerarramen (med alla andra sidredigeringselement), även om de faktiskt täcker över rätt komponenter i innehållsramen.

![Övertäckningar](assets/ui-overlays.png)

### Lager {#layer}

Ett lager är ett oberoende funktionspaket som kan aktiveras för att:

* Ange en annan vy av sidan
* Tillåt att du manipulerar och/eller interagerar med en sida

Lagren har avancerade funktioner för hela sidan, i motsats till specifika åtgärder för en enskild komponent.

AEM innehåller flera lager som redan har implementerats för sidredigering, till exempel redigering, förhandsgranskning och anteckning av lager.

>[!NOTE]
>
>Lager är ett kraftfullt koncept som påverkar användarens vy och interaktion med sidinnehållet. När du utvecklar egna lager måste du se till att lagret rensas när det avslutas.

### Lagerväxlare {#layer-switcher}

Med lagerväljaren kan du välja det lager som du vill använda. När det är stängt visas det lager som används.

Lagerväljaren är tillgänglig som en listruta från verktygsfältet (längst upp i fönstret, i redigeringsramen).

![Lagerväljaren](assets/ui-layer-switcher.png)

### Komponentverktygsfältet {#component-toolbar}

Varje instans av en komponent visar verktygsfältet när användaren klickar på det (antingen en gång eller med ett långsamt dubbelklick). Verktygsfältet innehåller de specifika åtgärder (till exempel kopiera, klistra in, öppna redigerare) som är tillgängliga för komponentinstansen på sidan.

Beroende på vilket utrymme som är tillgängligt placeras komponentens verktygsfält i det övre, eller nedre, högra hörnet av respektive komponent.

![Komponentverktygsfältet](assets/ui-component-toolbar.png)

## Ytterligare information {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

Mer teknisk information finns i [JS-dokumentationsuppsättningen](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html) för sidredigeraren.
