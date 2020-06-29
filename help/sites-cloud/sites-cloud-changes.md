---
title: Viktiga ändringar av AEM Sites i AEM Cloud Service
description: 'Viktiga ändringar av AEM Sites i AEM Cloud Service '
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 11%

---


# Viktiga ändringar i AEM Sites as a Cloud Service {#notable-changes}

AEM Sites som Cloud Service tillhandahåller upplevelsehanteringsfunktioner som en del av molnbaserade AEM som en Cloud Service-plattform. Förutom de viktigaste fördelarna med AEM som Cloud Service, till exempel molnbaserad skalbarhet, drifttid och ständigt uppdaterade, erbjuder AEM Sites som Cloud Service också ett antal webbplatsspecifika ändringar och tillägg.

>[!NOTE]
>Det här dokumentet markerar de anmärkningsvärda ändringarna av AEM Sites. Om du vill se ändringar som gäller för AEM som Cloud Service och andra moduler går du till:
>
>* [En introduktion till Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* En [översikt över AEM som en Cloud Service - Vad är nytt och Vad är annorlunda?](/help/overview/what-is-new-and-different.md)
>* [Arkitekturen](/help/core-concepts/architecture.md) i Adobe Experience Manager as a Cloud Service
>* [Noterbara ändringar i AEM som Cloud Service (versionsinformation)](/help/release-notes/aem-cloud-changes.md)
>* [Betydande ändringar av AEM Assets som en Cloud Service](/help/assets/assets-cloud-changes.md)
>* [AEM Assets som Cloud Service](/help/assets/overview.md)
>* [Självstudiekurser om Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)


Förändringarna och tilläggen i AEM Sites som Cloud Service är följande:

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

AEM som Cloud Service är alltid aktiverat och alltid uppdaterat. För att uppnå detta krävs att AEM-databasen skiljs åt i oföränderligt och muterbart innehåll och att åtkomst till oföränderligt innehåll förbjuds vid körning. Mer information om muterbart och oföränderligt innehåll finns i [Mutable vs. Immutable Area of the Repository](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

På grund av att det inte går att komma åt innehåll som inte kan ändras under körning är följande AEM Sites-åtgärder inte tillgängliga under körning:

* i18n-ordlisteöversättning
* Utvecklarläge i sidredigeraren i AEM Sites

Dessa funktioner kan användas via lokala, fristående utvecklarinstanser av AEM som Cloud Service för att uppdatera innehåll och kod i AEM som en Cloud Services-GIT-databas, men inte i värdbaserade körningsmiljöer.
