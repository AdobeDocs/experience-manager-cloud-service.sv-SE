---
title: Viktiga ändringar av AEM Sites i AEM Cloud Service
description: Viktiga ändringar av AEM Sites i AEM Cloud Service
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 15%

---

# Viktiga ändringar i AEM Sites as a Cloud Service {#notable-changes}

AEM Sites som Cloud Service tillhandahåller upplevelsehanteringsfunktioner som en del av den molnbaserade AEM som en Cloud Service-plattform. Förutom de viktigaste fördelarna med AEM som Cloud Service, till exempel molnbaserad skalbarhet, drifttid och ständigt uppdaterade, erbjuder AEM Sites som Cloud Service också ett antal platsspecifika ändringar och tillägg.

>[!NOTE]
>Det här dokumentet markerar de anmärkningsvärda ändringarna av AEM Sites. Om du vill ändra AEM som en Cloud Service och andra moduler läser du:
>
>* [En introduktion till Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* En [översikt över AEM som en Cloud Service - What is New and What is Different](/help/overview/what-is-new-and-different.md)
* [Arkitekturen](/help/core-concepts/architecture.md) i Adobe Experience Manager as a Cloud Service
* [Viktiga ändringar i AEM as a Cloud Service (versionsinformation)](/help/release-notes/aem-cloud-changes.md)
* [Viktiga ändringar i AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Nu kommer AEM Assets as a Cloud Service](/help/assets/overview.md)
* [Självstudiekurser om Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


Ändringarna och tilläggen i AEM Sites som Cloud Service är följande:

* [Asynkrona sidåtgärder](#asynchronous-page-operations)
* [Ny referenswebbplats och självstudiekurs](#new-reference-site-and-tutorial)

## Asynkrona sidåtgärder {#asynchronous-page-operations}

I AEM Cloud-tjänsten har åtgärder som traditionellt har blockerat gränssnittet delats upp i mindre åtgärder som körs i bakgrunden.

* Flytta sidor
* Rulla ut sidor

Initieraren av sådana åtgärder kan kontrollera deras status i ett nytt användargränssnitt på `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
Användaren av systemet behöver inte göra några ändringar för att kunna använda den här nya funktionen. Här noteras helt enkelt en förändring i beteendet jämfört med tidigare lokala versioner av AEM.

## Ny referenswebbplats och självstudiekurs {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), en ny AEM referensplats, har uppdaterats och publicerats för att återspegla bästa praxis för att skapa en webbplats med AEM och den omfattande uppsättning funktioner, komponenter och distributionsmodeller som finns i AEM. Den nya referenswebbplatsen och [den medföljande självstudiekursen](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) innehåller grundläggande ämnen som projektinställningar, kärnkomponenter, redigerbara mallar, klientbibliotek och komponentutveckling med Adobe Experience Manager Sites.

Tidigare installerades We.Retail som standard med AEM (förutom när det startades i produktionsläge).  Nu installeras ingen referensplats som standard.  I stället anges den [git repo](https://github.com/adobe/aem-guides-wknd/) och [medföljande självstudiekursen](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) med den uppdaterade koden för WKND-referensplatsen.

## Funktioner som inte är tillgängliga vid körning {#capabilities-not-available-at-runtime}

AEM som en Cloud Service är alltid aktiverad och alltid uppdaterad. För att uppnå detta måste AEM vara åtskild i oföränderligt och muterbart innehåll, och åtkomst till oföränderligt innehåll måste förbjudas vid körning. Mer information om muterbart eller oföränderligt innehåll finns i [Mutable vs. Immutable Areas of the Repository](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

På grund av att det inte går att komma åt innehåll som inte kan ändras under körning är följande AEM Sites-åtgärder inte tillgängliga under körning:

* i18n-ordlisteöversättning
* Utvecklarläge i AEM Sites Page Editor

Dessa funktioner kan användas via lokala, fristående utvecklarinstanser av AEM som en Cloud Service för att uppdatera innehåll och kod i AEM som en Cloud Services-GIT-databas, men inte i värdbaserade körningsmiljöer.
