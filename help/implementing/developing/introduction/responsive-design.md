---
title: Responsiv design
description: Med responsiv design kan samma upplevelser visas effektivt på flera enheter i flera olika orienteringar
translation-type: tm+mt
source-git-commit: a3b2a66958fd8d3a68b450938c5c18053f00b998
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Responsiv design {#responsive-design}

Utforma era upplevelser så att de anpassar sig till den kundvisningsruta där de visas. Med responsiv design kan samma sidor visas effektivt på flera enheter i båda riktningarna. I följande bild visas några sätt på vilka en sida kan reagera på ändringar i visningsrutans storlek:

* Layout: Använd enspaltig layout för mindre visningsrutor och flerspaltig layout för större visningsrutor.
* Textstorlek: Använd större textstorlek (vid behov till exempel rubriker) i större visningsrutor.
* Innehåll: Inkludera endast det viktigaste innehållet när det visas på mindre enheter.
* Navigering: Enhetsspecifika verktyg finns för åtkomst till andra sidor.
* Bilder: Serverar bildåtergivningar som är lämpliga för klientvisningsrutan enligt fönsterdimensionerna.

![Exempel på responsiv design](assets/responsive-example.png)

Utveckla Adobe Experience Manager-program (AEM) som genererar HTML5 som anpassar sig till olika fönsterstorlekar och orienteringar. Följande intervall med visningsrutebredder motsvarar till exempel olika enhetstyper och orienteringar

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

W3C-gruppen innehåller [Media Queries](https://www.w3.org/TR/css3-mediaqueries/)-rekommendationen som beskriver denna CSS3-funktion och syntaxen.

### CSS-filen {#creating-the-css-file} skapas

I CSS-filen definierar du mediefrågor baserat på egenskaperna för de enheter som du har som mål. Följande implementeringsstrategi är effektiv för att hantera format för varje mediefråga:

* Använd en [klientbiblioteksmapp](clientlibs.md) för att definiera den CSS som ska monteras när sidan återges.
* Definiera varje mediefråga och tillhörande format i separata CSS-filer. Det är användbart att använda filnamn som representerar enhetsfunktionerna i mediefrågan.
* Definiera format som är gemensamma för alla enheter i en separat CSS-fil.
* I css.txt-filen i mappen Klientbibliotek ordnar du CSS-listfilerna så som krävs i den sammansatta CSS-filen.

I [WKND-självstudiekursen](develop-wknd-tutorial.md) används den här strategin för att definiera format i webbplatsdesignen. CSS-filen som används av WKND finns på `/apps/wknd/clientlibs/clientlib-grid/less/grid.less`.
