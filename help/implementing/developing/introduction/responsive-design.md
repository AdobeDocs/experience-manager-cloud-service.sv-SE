---
title: Responsiv design
description: Med responsiv design kan samma upplevelser visas effektivt på flera enheter i flera olika orienteringar.
exl-id: be645062-d6d6-45a2-97dc-d8aa235539b8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---

# Responsiv design {#responsive-design}

Utforma era upplevelser så att de anpassar sig till den kundvisningsruta där de visas. Med responsiv design kan samma sidor visas effektivt på flera enheter i båda riktningarna. I följande bild visas några sätt på vilka en sida kan reagera på ändringar i visningsrutans storlek:

* Layout: Använd layouter med en kolumn för mindre visningsrutor och layouter med flera kolumner för större visningsrutor.
* Textstorlek: Använd större textstorlek (vid behov, t.ex. rubriker) i större visningsrutor.
* Innehåll: Inkludera endast det viktigaste innehållet när det visas på mindre enheter.
* Navigering: Enhetsspecifika verktyg finns för åtkomst till andra sidor.
* Bilder: Serverar bildåtergivningar som är lämpliga för klientvisningsrutan enligt fönsterdimensionerna.

![Exempel på responsiv design](assets/responsive-example.png)

Utveckla Adobe Experience Manager-program (AEM) som genererar HTML5 som anpassar sig efter olika fönsterstorlekar och orienteringar. Följande intervall med visningsrutebredder motsvarar till exempel olika enhetstyper och orienteringar

* Maximal bredd på 480 pixlar (telefon, stående)
* Maximal bredd på 767 pixlar (telefon, liggande)
* Bredd mellan 768 pixlar och 979 pixlar (surfplatta, stående)
* Bredd mellan 980 pixlar och 1 199 pixlar (surfplatta, liggande)
* Bredd 1200px eller högre (skrivbord)

Mer information om hur du implementerar responsiva designbeteenden finns i följande avsnitt:

* [Mediefrågor](#using-media-queries)
* [Flytande stödraster](#developing-a-fluid-grid)
* [Adaptiva bilder](#using-adaptive-images)

När du designar kan du använda verktygsfältet **Emulator** för att förhandsgranska sidorna för olika skärmstorlekar.

## Innan du utvecklar {#before-you-develop}

Innan du utvecklar det AEM programmet som stöder dina webbsidor bör du fatta flera designbeslut. Du måste till exempel ha följande information:

* De enheter ni riktar er mot
* Storleken på målvisningsrutan
* Sidlayouterna för varje målvisningsrutestorlek

### Programstruktur {#application-structure}

Den typiska AEM programstrukturen har stöd för alla responsiva designimplementeringar:

* Sidkomponenter finns under `/apps/<application_name>/components`
* Mallar finns under `/apps/<application_name>/templates`

## Använda mediefrågor {#using-media-queries}

Mediefrågor möjliggör selektiv användning av CSS-format för sidåtergivning. Med AEM utvecklingsverktyg och funktioner kan du effektivt och effektivt implementera mediefrågor i dina program.

W3C-gruppen tillhandahåller rekommendationen [Mediefrågor](https://www.w3.org/TR/css3-mediaqueries/) som beskriver den här CSS3-funktionen och syntaxen.

### Skapa CSS-filen {#creating-the-css-file}

I CSS-filen definierar du mediefrågor baserat på egenskaperna för de enheter som du har som mål. Följande implementeringsstrategi är effektiv för att hantera format för varje mediefråga:

* Använd en [klientbiblioteksmapp](clientlibs.md) för att definiera den CSS som sätts samman när sidan återges.
* Definiera varje mediefråga och tillhörande format i separata CSS-filer. Det är användbart att använda filnamn som representerar enhetsfunktionerna i mediefrågan.
* Definiera format som är gemensamma för alla enheter i en separat CSS-fil.
* I css.txt-filen i mappen Klientbibliotek ordnar du CSS-listfilerna så som krävs i den sammansatta CSS-filen.

I [WKND-självstudien](develop-wknd-tutorial.md) används den här strategin för att definiera format i webbplatsdesignen. CSS-filen som används av WKND finns på `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.

### Använda mediefrågor med AEM sidor {#using-media-queries-with-aem-pages}

[WKND-exempelprojektet](/help/implementing/developing/introduction/develop-wknd-tutorial.md) och [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) använder [Page Core Component,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/page.html), som inkluderar klientlibs via sidprincipen.

Om din egen sidkomponent inte är baserad på Page Core-komponenten kan du även inkludera klientbiblioteksmappen i HTML- eller JSP-skriptet för den. Om du gör det genereras och refereras CSS-filen med de mediefrågor som behövs för att det responsiva rutnätet ska fungera.

#### HTL {#htl}

```html
<sly data-sly-use.clientlib="${'/libs/granite/sightly/templates/clientlib.html'}">
<sly data-sly-call="${clientlib.all @ categories='apps.weretail.all'}"/>
```

#### JSP {#jsp}

```xml
<ui:includeClientLib categories="apps.weretail.all"/>
```

JSP-skriptet genererar följande HTML-kod som refererar till formatmallarna:

```xml
<link rel="stylesheet" href="/etc/designs/weretail/clientlibs-all.css" type="text/css">
<link href="/etc/designs/weretail.css" rel="stylesheet" type="text/css">
```

## Förhandsgranska för specifika enheter {#previewing-for-specific-devices}

Med emulatorn kan du förhandsgranska sidorna i olika visningsrutestorlekar så att du kan testa beteendet i din responsiva design. När du redigerar en sida i platskonsolen kan du trycka eller klicka på ikonen **Emulator** för att visa emulatorn.

![Emulatorikonen i verktygsfältet](assets/emulator-icon.png)

I emulatorns verktygsfält kan du trycka eller klicka på ikonen **Enheter** för att visa en nedrullningsbar meny där du kan välja en enhet. När du väljer en enhet ändras sidan så att den anpassas till visningsrutans storlek.

![Emulatorverktygsfältet](assets/emulator.png)

### Ange enhetsgrupper {#specifying-device-groups}

Om du vill ange de enhetsgrupper som visas i listan **Enheter** lägger du till en `cq:deviceGroups` -egenskap i noden `jcr:content` på mallsidan på platsen. Värdet för egenskapen är en array med sökvägar till enhetsgruppsnoderna.

Exempelvis är mallsidan för WKND-webbplatsen `/conf/wknd/settings/wcm/template-types/empty-page/structure`. Noden `jcr:content` under den innehåller följande egenskap:

* Namn: `cq:deviceGroups`
* Typ: `String[]`
* Värde: `mobile/groups/responsive`

Enhetsgruppnoderna finns i mappen `/etc/mobile/groups`.

## Responsiva bilder {#responsive-images}

Responsiva sidor anpassar sig dynamiskt till den enhet som de återges på, vilket ger en bättre upplevelse för användaren. Men det är också viktigt att resurserna optimeras till brytpunkten och enheten för att minimera sidinläsningstiden.

[Core Component Image Component Component ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html) har funktioner som adaptiv bildmarkering.

* Som standard använder Image-komponenten [Adaptive Image Server](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/adaptive-image-servlet.html) för att leverera rätt återgivning.
* [Webboptimerad bildleverans](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) är också tillgängligt via en enkel kryssruta i policyn, som levererar bildresurser från DAM i WebP-format och kan minska hämtningsstorleken för en bild med i genomsnitt cirka 25 %.

## Layoutbehållaren {#layout-container}

Med AEM Layout Container kan du effektivt implementera responsiv layout för att anpassa sidans dimensioner till klientens visningsruta.

Se dokumentet [Konfigurera layoutbehållare och layoutläge](/help/sites-cloud/administering/responsive-layout.md) för mer information om hur layoutbehållaren fungerar och hur du aktiverar responsiva layouter för ditt innehåll.
