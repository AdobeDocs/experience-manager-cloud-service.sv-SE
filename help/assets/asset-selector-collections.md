---
title: Resursväljarsamlingar
description: Arbeta med resursväljarsamlingar.
role: Admin,User
exl-id: 1687e7d5-eb7e-4eb7-8747-e5dc6afacd5b
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Resursväljarsamlingar {#asset-selector-collections}

En samling är en uppsättning resurser, mappar eller andra samlingar i resursväljaren. Använd samlingar för att dela resurser mellan användare. Till skillnad från mappar kan en samling innehålla resurser från olika platser.

Micro Front-end-samlingar i resursväljaren är tillgängliga direkt i skrivskyddat läge. Den hämtar resurser och samlingar direkt från [!DNL Experience Manager Assets]-databasen som du har åtkomst till.

>[!NOTE]
>
>Kontrollera att du har behörighet att komma åt en [!DNL Experience Manager Assets] [imsOrg](/help/assets/asset-selector-properties.md) och samlingar.

Micro Front-end-samlingar i resursväljaren är tillgängliga direkt i skrivskyddat läge. Den hämtar resurser och samlingar direkt från Experience Manager Assets-databasen som du har tillgång till och ärver egenskaperna för offentliga och privata mappar från din Experience Manager Assets-databas. Se mer om att [skapa en offentlig eller privat samling i Assets-vyn](/help/assets/manage-collections-assets-view.md#create-collection).

Du kan visa samlingar i resursväljaren både i vyn Rälar och i vyn modala resurser.

![Samlingar i rälsvy](assets/collections-rail-modal-view.png)

<!--
Additionally, you can [customize](/help/assets/asset-selector-customization.md) the `featureSet` property to enable or disable collections in Asset Selector. See [enable or disable Collections tab](#enable-disable-collections-tab).-->

Du kan också anpassa urvalet av resurser på fliken Samlingar. Om du vill göra det kan du anpassa det med `handleSelection`. Se [Hantera urval av Assets med objektschema](/help/assets/asset-selector-customization.md#handling-selection).

## Visa samlingar {#view-collections}

Med resursväljaren kan du visa samlingar i antingen en ![listvy](assets/do-not-localize/list-view.png) eller en ![stödrastervy](assets/do-not-localize/grid-view.png) . Se [typer av vy i Resursväljaren](overview-asset-selector.md#types-of-view).

## Dra och släpp resurser till samlingen {#collection-drag-and-drop}

Du kan dra och släppa en resurs i samlingar direkt från vyn [!DNL Assets as a Cloud Service] i redigeringsmiljön. Det gör du genom att dra resursen från fliken Assets till arbetsytan Samlingar i resursväljarprogrammet för att skapa avancerade program.

>[!NOTE]
>
>* Det går bara att dra och släppa en resurs i rälsvy.
>* Du kan bara dra och släppa filer (resurser) och inte mappar.

Å andra sidan kan du även [aktivera eller inaktivera dra och släpp av resurser i samlingarna](asset-selector-customization.md#enable-disable-drag-and-drop) direkt.

## Inaktivera markering av resurs i samlingar {#disable-selection-collection}

Inaktivera markering används för att dölja eller inaktivera att resurser eller mappar kan markeras. Den döljer kryssrutan välj från kortet eller resursen som inte gör att den markeras. Se [inaktivera markering](/help/assets/asset-selector-customization.md#disable-selection).

## Aktivera eller inaktivera fliken Samlingar {#enable-disable-collections-tab}

Med resursväljaren kan du anpassa komponenterna efter behov och användbarhet. Om du vill aktivera eller inaktivera fliken Samlingar i Resursväljaren kan du använda egenskapen `featureSet` på följande sätt:

* **Aktivera fliken Samlingar:** Om du vill aktivera fliken Samlingar måste du ange `collections` som värde för arrayen. Fliken Samlingar är som standard aktiverad utanför rutan för alla användare. Exempel: `featureSet:["collections"]`
* **Inaktivera fliken Samlingar:** Om du vill inaktivera fliken Samlingar måste du ange en tom array som värde. Exempel: `featureSet:[ ]`

>[!MORELIKETHIS]
>
>* [Anpassningar av resursväljare](/help/assets/asset-selector-customization.md)
>* [Integrera resursväljare med olika program](/help/assets/integrate-asset-selector.md)
>* [Egenskaper för resursväljare](/help/assets/asset-selector-properties.md)
