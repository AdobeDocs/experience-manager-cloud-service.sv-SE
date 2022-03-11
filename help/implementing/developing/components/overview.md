---
title: Komponenter - översikt
description: Komponenter är modulära enheter som har vissa funktioner för att presentera ditt innehåll på din webbplats
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Komponenter - översikt {#components-overview}

På den här sidan finns en översikt över Adobe Experience Manager (AEM) komponenter som [används för att skapa sidor](/help/sites-cloud/authoring/fundamentals/components.md).

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
* utvecklas med [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html).
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

[De AEM kärnkomponenterna](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) är en uppsättning standardiserade WCM-komponenter (Web Content Management) för AEM som snabbar upp utvecklingstiden och minskar underhållskostnaderna för dina webbplatser.

Kärnkomponenterna är AEM as a Cloud Service och [WKND - självstudiekurs](/help/implementing/developing/introduction/develop-wknd-tutorial.md) visar hur du implementerar och använder komponenter. Komponenterna levereras med all källkod och kan användas som de är eller som startpunkter för ändrade eller utökade komponenter.

### Visa tillgängliga komponenter {#viewing-available-components}

Använd kommandot [Komponentkonsol](/help/sites-cloud/authoring/features/components-console.md).

Du kan också använda CRXDE Lite för att få en lista över alla komponenter som är tillgängliga i databasen.

1. I **[!UICONTROL CRXDE Lite]**, markera **[!UICONTROL Tools]** från verktygsfältet och sedan **[!UICONTROL Query]** som öppnar **[!UICONTROL Query]** -fliken.

1. I **[!UICONTROL Query]** flik, välja `XPath` as **[!UICONTROL Type]**.

1. I **[!UICONTROL Query]** indatafält, ange följande sträng:

   `//element(*, cq:Component)`

1. Klicka **[!UICONTROL Execute]** och komponenterna visas.
