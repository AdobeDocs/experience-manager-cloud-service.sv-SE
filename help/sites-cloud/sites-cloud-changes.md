---
title: Betydande ändringar av AEM Sites i AEM Cloud-tjänsten
description: Förstå hur man redigerar med och administrerar AEM Sites as a Cloud Service och om betydande ändringar av AEM Sites i AEM Cloud Service.
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 3761019b42ddc4b3a6cc904afe91b47eb3d99ac6
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 15%

---


# Betydande förändringar i AEM Sites as a Cloud Service {#notable-changes}

AEM Sites as a Cloud Service har funktioner för upplevelsehantering som en del av AEM as a Cloud Service molnbaserade plattform. Förutom de viktigaste fördelarna med AEM as a Cloud Service, som molnbaserad skalbarhet, drifttid och ständigt uppdaterade, erbjuder AEM Sites as a Cloud Service även flera platsspecifika ändringar och tillägg.

>[!NOTE]
>Det här dokumentet markerar de anmärkningsvärda ändringarna av AEM Sites. Om du vill ändra AEM as a Cloud Service och andra moduler går du till:
>
>* [En introduktion till Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* En [översikt över AEM as a Cloud Service - Vad är nytt och vad är annorlunda](/help/overview/what-is-new-and-different.md)
>* [Arkitekturen](/help/overview/architecture.md) i Adobe Experience Manager as a Cloud Service
>* [Viktiga ändringar i AEM as a Cloud Service (versionsinformation)](/help/release-notes/aem-cloud-changes.md)
>* [Viktiga ändringar i AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
>* [Nu kommer AEM Assets as a Cloud Service](/help/assets/overview.md)
>* [Självstudiekurser om Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

Ändringarna och tilläggen i AEM Sites as a Cloud Service är följande:

* [Asynkrona sidåtgärder](#asynchronous-page-operations)
* [Ny referenswebbplats och självstudiekurs](#new-reference-site-and-tutorial)

## Asynkrona sidåtgärder {#asynchronous-page-operations}

I AEM Cloud-tjänsten har åtgärder som traditionellt har blockerat gränssnittet delats upp i mindre åtgärder som körs i bakgrunden.

* Flytta sidor
* Rulla ut sidor

<!--
The initiator of such actions can check their status in a new UI at `/mnt/overlay/dam/gui/content/asyncjobs.html`.
-->

Du kan visa status för asynkrona jobb från kontrollpanelen [Bakgrundsåtgärder](/help/operations/asynchronous-jobs.md).

>[!NOTE]
>
>Användaren av systemet behöver inte ändra den här nya funktionen. Här noteras helt enkelt en förändring i beteendet jämfört med tidigare lokala versioner av AEM.

## Ny referenswebbplats och självstudiekurs {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/), en ny referenswebbplats för AEM, har uppdaterats och publicerats för att återspegla bästa praxis för att skapa en webbplats med AEM, och med den omfattande uppsättningen funktioner, komponenter och distributionsmodeller som finns i AEM. Den nya referenswebbplatsen och den [medföljande självstudiekursen](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) innehåller grundläggande ämnen som projektinställningar, kärnkomponenter, redigerbara mallar, klientbibliotek och komponentutveckling med Adobe Experience Manager Sites.

Tidigare installerades We.Retail som standard med AEM (förutom när det startades i produktionsläge). I AEM as a Cloud Service installeras ingen referensplats som standard. Istället anges den [Git-repo](https://github.com/adobe/aem-guides-wknd/) och [åtföljande självstudiekursen](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) med den uppdaterade WKND-referensplatskoden.

## Funktioner som inte är tillgängliga vid körning {#capabilities-not-available-at-runtime}

AEM as a Cloud Service är alltid aktiverat och alltid uppdaterat. För att uppnå detta krävs att AEM-databasen skiljs åt i oföränderligt och muterbart innehåll och att åtkomst till oföränderligt innehåll förbjuds vid körning. Mer information om ändringsbart och icke ändringsbart innehåll finns i [Ändringsbara kontra oföränderliga områden i databasen](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

På grund av att det inte går att komma åt innehåll som inte kan ändras under körning är följande AEM Sites-åtgärder inte tillgängliga under körning:

* i18n-ordlisteöversättning
* Utvecklarläge i AEM Sites Page Editor

Dessa funktioner kan användas via lokala, fristående utvecklarinstanser av AEM as a Cloud Service för att uppdatera innehåll och kod i AEM as a Cloud Service GIT-databas, men inte i värdbaserade körningsmiljöer.
