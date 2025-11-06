---
title: Komponenter - översikt
description: Komponenter är modulära enheter som har vissa funktioner för att presentera ditt innehåll på din webbplats
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Komponenter - översikt {#components-overview}

Den här sidan innehåller en översikt över Adobe Experience Manager-komponenter (AEM), till exempel de [som används för sidredigering](/help/sites-cloud/authoring/page-editor/components.md).

## Vad är komponenter? {#what-are-components}

* Modulära enheter som utnyttjar specifika funktioner för att presentera innehållet på webbplatsen.
* Återanvändbart.
* Utvecklas som självständiga enheter i en mapp i databasen.
* Har inga dolda konfigurationsfiler.
* De kan innehålla andra komponenter.
* De kan köras var som helst i alla AEM-system och kan även begränsas till att köras under specifika komponenter.
* ha ett standardiserat användargränssnitt.
* Har redigeringsbeteende som kan konfigureras.
* Använd dialogrutor som har skapats med delelement som baseras på GRE-komponenter.
* De har utvecklats med [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html).
* De kan utvecklas för att skapa anpassade komponenter som utökar standardfunktionerna.

Eftersom komponenterna är modulära kan du:

* Utveckla en ny komponent på den lokala instansen.
* Driftsätt den i testmiljön.
* Distribuera det till redigeringsmiljön där författare och/eller administratörer kan lägga till och konfigurera innehåll.
* Distribuera det i publiceringsmiljöer där de används för att återge innehåll för besökare på webbplatsen.

Varje AEM-komponent:

* Är en resurstyp.
* Är en samling skript som helt och hållet realiserar en viss funktion.
* Kan fungera fristående, vilket betyder antingen inom AEM eller en portal.

## Grundläggande komponenter i AEM {#aem-core-components}

[AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) är en uppsättning standardiserade WCM-komponenter (Web Content Management) för AEM som snabbar upp utvecklingstiden och minskar underhållskostnaderna för dina webbplatser.

Core Components ingår i AEM as a Cloud Service och [WKND Tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md) visar hur du implementerar och använder komponenter. Komponenterna levereras med all källkod och kan användas som de är eller som startpunkter för ändrade eller utökade komponenter.

### Visa tillgängliga komponenter {#viewing-available-components}

Använd [komponentkonsolen](/help/sites-cloud/authoring/components-console.md) om du vill se en översikt över alla tillgängliga komponenter i din AEM-instans.

Du kan också använda CRXDE Lite för att få en lista över alla komponenter som är tillgängliga i databasen.

1. I **[!UICONTROL CRXDE Lite]** väljer du **[!UICONTROL Tools]** i verktygsfältet och sedan **[!UICONTROL Query]**, som öppnar fliken **[!UICONTROL Query]**.

1. Välj **[!UICONTROL Query]** som `XPath` på fliken **[!UICONTROL Type]**.

1. Ange följande sträng i indatafältet **[!UICONTROL Query]**:

   `//element(*, cq:Component)`

1. Klicka på **[!UICONTROL Execute]** så visas komponenterna.
