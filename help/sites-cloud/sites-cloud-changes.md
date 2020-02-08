---
title: Betydande ändringar av AEM-webbplatser i AEM Cloud-tjänsten
description: 'Betydande ändringar av AEM-webbplatser i AEM Cloud-tjänsten '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Betydande ändringar av AEM-webbplatser som en molntjänst {#notable-changes}

AEM Sites som en molntjänst tillhandahåller upplevelsehanteringsfunktioner som en del av molnbaserade AEM som en plattform för molntjänster. Förutom de viktigaste fördelarna med AEM som molntjänst, till exempel molnbaserad skalbarhet, drifttid och ständigt uppdaterade, erbjuder AEM Sites som molntjänst även ett antal webbplatsspecifika ändringar och tillägg.

>[!NOTE]
>Det här dokumentet belyser de betydande ändringarna av AEM Sites. Allmänna ändringar av AEM i molnet finns här:
>
>* [Betydande ändringar av Adobe Experience Manager (AEM) som en molntjänst](/help/release-notes/aem-cloud-changes.md)


Ändringar och tillägg i AEM Sites som en molntjänst är följande:

* [Asynkrona sidåtgärder](#asynchronous-page-operations)
* [Ny referenswebbplats och självstudiekurs](#new-reference-site-and-tutorial)

## Asynkrona sidåtgärder {#asynchronous-page-operations}

I AEM Cloud-tjänsten har åtgärder som traditionellt har blockerat gränssnittet delats upp i mindre åtgärder som körs i bakgrunden.

* Flytta sidor
* Rulla ut sidor

Initieraren av sådana åtgärder kan kontrollera deras status i ett nytt användargränssnitt på `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>Användaren av systemet behöver inte göra några ändringar för att kunna använda den här nya funktionen. Här noteras det helt enkelt som en förändring av beteendet jämfört med tidigare lokala versioner av AEM.

## Ny referenswebbplats och självstudiekurs {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), en ny AEM-referenswebbplats, har uppdaterats och publicerats för att återspegla bästa praxis för att skapa en webbplats med AEM, samt den omfattande uppsättning funktioner, komponenter och distributionsmodeller som finns i AEM. Den nya referenswebbplatsen och den [medföljande självstudiekursen](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) omfattar grundläggande ämnen som projektinställningar, kärnkomponenter, redigerbara mallar, klientbibliotek och komponentutveckling med Adobe Experience Manager Sites.

Tidigare installerades We.Retail som standard med AEM (förutom när det startades i produktionsläge).  Nu installeras ingen referensplats som standard.  I stället anges [Git-repo](https://github.com/adobe/aem-guides-wknd/) och [tillhörande självstudiekurs](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) med den uppdaterade koden för WKND-referensplatsen.

## Funktioner som inte är tillgängliga vid körning {#capabilities-not-available-at-runtime}

AEM som molntjänst är alltid aktiverat och alltid uppdaterat. För att uppnå detta krävs att AEM-databasen skiljs åt i oföränderligt och muterbart innehåll och att åtkomst till oföränderligt innehåll förbjuds vid körning. Mer information om muterbart och oföränderligt innehåll finns i [Mutable vs. Immutable Area of the Repository](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

På grund av att det inte går att komma åt innehåll som inte kan ändras under körning är följande AEM Sites-åtgärder inte tillgängliga under körning:

* i18n-ordlisteöversättning
* Utvecklarläge i sidredigeraren AEM Sites

Dessa funktioner kan användas via lokala, fristående utvecklarinstanser av AEM som en molntjänst för att uppdatera innehåll och kod i AEM som en GIT-databas för molntjänster, men inte i värdbaserade körningsmiljöer.
