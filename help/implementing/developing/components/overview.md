---
title: Komponenter - översikt
description: Komponenter är modulära enheter som har vissa funktioner för att presentera ditt innehåll på din webbplats
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---


# Komponenter - översikt {#components-overview}

På den här sidan finns en översikt över Adobe Experience Manager-komponenter (AEM), t.ex. de som [används för att skapa](/help/sites-cloud/authoring/fundamentals/components.md)sidor.

## Vad är komponenter? {#what-are-components}

Komponenterna i AEM är:

* Modulära enheter som utnyttjar specifika funktioner för att presentera innehållet på webbplatsen.
* Kan återanvändas.
* Utvecklas som självständiga enheter i en mapp i databasen.
* Har inga dolda konfigurationsfiler.
* Kan innehålla andra komponenter.
* Kan köras var som helst i vilket AEM som helst och kan även begränsas till att köras under särskilda komponenter.
* ha ett standardiserat användargränssnitt.
* Har redigeringsbeteende som kan konfigureras.
* Använd dialogrutor som är byggda med delelement som är baserade på GRE-komponenter.
* Utvecklas med [HTML](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html).
* Kan utvecklas för att skapa anpassade komponenter som utökar standardfunktionerna.

Eftersom komponenterna är modulära kan du:

* Utveckla en ny komponent på den lokala instansen.
* Driftsätt den i testmiljön.
* Distribuera det till redigeringsmiljön där författare och/eller administratörer kan lägga till och konfigurera innehåll.
* Distribuera den i publiceringsmiljön där de används för att återge innehåll för besökare på webbplatsen.

Varje AEM:

* Är en resurstyp.
* Är en samling skript som helt och hållet realiserar en viss funktion.
* Kan fungera fristående, vilket betyder antingen AEM eller en portal.

## AEM kärnkomponenter {#aem-core-components}

[De AEM kärnkomponenterna](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) är en uppsättning standardiserade WCM-komponenter (Web Content Management) för AEM som snabbar upp utvecklingstiden och minskar underhållskostnaderna för dina webbplatser.

Core Components har AEM som Cloud Service och [WKND-självstudiekursen](/help/implementing/developing/introduction/develop-wknd-tutorial.md) visar hur du implementerar och använder komponenter. Komponenterna levereras med all källkod och kan användas som de är eller som startpunkter för ändrade eller utökade komponenter.

### Visa tillgängliga komponenter {#viewing-available-components}

Använd [komponentkonsolen](/help/sites-cloud/authoring/features/components-console.md)om du vill se en översikt över alla tillgängliga komponenter i AEM.

Du kan också använda CRXDE Lite för att få en lista över alla komponenter som är tillgängliga i databasen.

1. I **[!UICONTROL CRXDE Lite]** väljer du **[!UICONTROL Tools]** från verktygsfältet **[!UICONTROL Query]** så öppnas **[!UICONTROL Query]** fliken.

1. Välj **[!UICONTROL Query]** som på `XPath` fliken **[!UICONTROL Type]**.

1. Ange följande sträng i **[!UICONTROL Query]** indatafältet:

   `//element(*, cq:Component)`

1. Klicka **[!UICONTROL Execute]** så visas komponenterna.

