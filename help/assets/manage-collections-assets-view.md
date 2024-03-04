---
title: Hantera samlingar
description: En samling är en uppsättning resurser i vyn Experience Manager Assets. Använd samlingar för att dela resurser mellan användare.
source-git-commit: c3076ce35128c147ce2056d11d9305d9a9456636
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Hantera samlingar {#manage-collections}

>[!CONTEXTUALHELP]
>id="assets_collections"
>title="Hantera samlingar"
>abstract="En samling är en uppsättning resurser, mappar eller andra samlingar i resursvyn. Använd samlingar för att dela resurser mellan användare. Till skillnad från mappar kan en samling innehålla resurser från olika platser. Du kan dela flera samlingar med en användare. Varje samling innehåller referenser till resurser. Resursernas referensintegritet bevaras i alla samlingar."

En samling är en uppsättning resurser, mappar eller andra samlingar i vyn Adobe Experience Manager Assets. Använd samlingar för att dela resurser mellan användare.

Till skillnad från mappar kan en samling innehålla resurser från olika platser.

<!--
You can share collections with various users that are assigned different levels of privileges, including viewing, editing, and so on.
-->

Du kan dela flera samlingar med en användare. Varje samling innehåller referenser till resurser. Resursernas referensintegritet bevaras i alla samlingar.

![Samlingar](assets/collections.png)

Du kan utföra följande åtgärder för att hantera och använda samlingar:

* [Skapa en samling](#create-collection)

* [Lägga till resurser i en samling](#add-assets-to-collection)

* [Ta bort resurser från en samling](#remove-assets-from-collection)

* [Skapa en smart samling](#create-smart-collection)

* [Redigera en smart samling](#edit-smart-collection)

* [Visa och redigera samlingsmetadata](#view-edit-collection-metadata)

* [Dela länkar för samlingar](#share-collection-links)

* [Hämta en samling](#download-collection)

* [Ta bort en samling](#delete-collection)

## Skapa en samling {#create-collection}

Så här skapar du en samling:

1. Klicka **[!UICONTROL Collections]** i den vänstra listen och klicka sedan **[!UICONTROL Create Collection]**.

1. Ange en rubrik och en valfri beskrivning för samlingen.

1. Välj om du behöver skapa en privat samling eller en offentlig samling. En offentlig samling är tillgänglig för visning och redigering av alla användare. En privat samling är dock tillgänglig för skaparen och användare med administratörsbehörighet.

1. Klicka **[!UICONTROL Create]** för att skapa samlingen.

![Skapa samling](assets/create-collection.png)

<!--
   
   for viewing and editing only to users with the appropriate [permissions](#manage-collection-access).

-->

## Lägga till resurser i en samling {#add-assets-to-collection}

Så här lägger du till resurser i en samling:

1. Klicka **[!UICONTROL Assets]** i den vänstra listen och välj de resurser som du vill lägga till i en samling.

1. Klicka på **[!UICONTROL Add to Collection]**.

1. På [!UICONTROL Collections] väljer du de samlingar du vill lägga till de markerade resurserna i.

1. Klicka **[!UICONTROL Add]** om du vill lägga till resursen i de valda samlingarna.

## Ta bort resurser från en samling {#remove-assets-from-collection}

Så här tar du bort resurser från en samling:

1. Klicka **[!UICONTROL Collections]** i den vänstra listen för att visa en lista över samlingar.

1. Klicka på samlingen och markera objekt som du vill ta bort från samlingen.

1. Klicka på **[!UICONTROL Remove]**.

## Hantera en smart samling {#manage-smart-collection}

Spara sökresultaten som en smart samling för att dynamiskt uppdatera samlingens innehåll. Om det finns resurser som har lagts till i resursvyns databas och som passar de sökvillkor som angavs när den smarta samlingen skapades, uppdateras innehållet i den smarta samlingen automatiskt när du öppnar en smart samling.

### Skapa en smart samling {#create-smart-collection}

Så här skapar du en smart samling:

1. Klicka **[!UICONTROL Filter]** och [definiera sökvillkoren](search-assets-view.md#refine-search-results).

1. Klicka **[!UICONTROL Save as]** och sedan **[!UICONTROL Smart Collection]**.

   ![Skapa smart samling](assets/create-smart-collection.png)

1. På [!UICONTROL Create Smart Collection] anger du en rubrik och en beskrivning för den smarta samlingen.

1. Välj **[!UICONTROL Public Collection]** om du behöver alla användare för att komma åt samlingen. Välj **[!UICONTROL Private Collection]** om du behöver en begränsad grupp användare för att komma åt samlingen.

1. Klicka **[!UICONTROL Create]** för att skapa den smarta samlingen.

### Redigera en smart samling {#edit-smart-collection}

Så här redigerar du en smart samling:

1. Klicka **[!UICONTROL Collections]** i den vänstra listen och dubbelklicka sedan på namnet på samlingen som du vill redigera.

1. Klicka på **[!UICONTROL Edit Smart Collection]**.

1. På [!UICONTROL Edit Smart Collection Filters] dialogruta, [uppdatera sökvillkoren](search-assets-view.md#refine-search-results) för Smart Collection.

1. Klicka på **[!UICONTROL Save]**.

<!--

## Manage access to a Private collection {#manage-collection-access}

The permission management for collections function in the same manner as folders in [!DNL Assets view]. Administrators can manage the access levels for collections available in the repository. As an administrator, you can create user groups and assign permissions to those groups to manage access levels. You can also delegate the permission management privileges to user groups at the collection-level.

For more information, see [Manage permissions for folders and collections](manage-permissions.md).

-->

<!--

## Search a collection {#search-collections}

Click **[!UICONTROL Collections]** in the left rail and use the Search box to specify a text as the criteria to search for a collection. [!DNL Assets view] uses the specified text to search collection names, metadata including tags defined for a collection and returns appropriate results.

>[!NOTE]
>
>Assets view performs search in collections available at the root level. It does not perform search in assets and folders available in collections.

-->

## Visa och redigera samlingsmetadata {#view-edit-collection-metadata}

Samlingsmetadata omfattar data om samlingen, till exempel titel och beskrivning.

Så här visar och redigerar du samlingens metadata:

1. Klicka **[!UICONTROL Collections]** i den vänstra listen väljer du en samling och klickar på **[!UICONTROL Details]**.
1. Visa samlingens metadata med **[!UICONTROL Basic]** -fliken.
1. Ändra metadatafälten efter behov. Du kan ändra [!UICONTROL Title] och [!UICONTROL Description] fält.

![Samlingsmetadata](assets/collection-metadata.png)

## Dela länkar för samlingar {#share-collection-links}

[!DNL Assets view] gör att du kan skapa en länk och dela samlingar och resurser i samlingar med externa intressenter som inte har tillgång till [!DNL Assets view] program. Du kan definiera ett förfallodatum för länken och sedan dela det med andra via den kommunikationsmetod du föredrar, som e-post eller meddelandetjänster. Mottagarna av länken kan förhandsgranska resurser och hämta dem.

![Dela länk för resurser](assets/share-link-collections.png)

Mer information om hur du delar samlingslänkar med externa intressenter finns i [dela länkar för resurser](/help/assets/share-links-for-assets-view.md).

## Hämta en samling {#download-collection}

Så här hämtar du en samling:

1. Klicka **[!UICONTROL Collections]** till vänster.

1. Välj den samling du vill hämta och klicka på **[!UICONTROL Download]**.

1. På [!UICONTROL Downloading Asset] klickar du på **[!UICONTROL OK]**.

Samlingen laddas ned som en ZIP-fil på den lokala datorn.

## Ta bort en samling {#delete-collection}

Så här tar du bort en samling:

1. Klicka **[!UICONTROL Collections]** till vänster.

1. Markera den samling som du vill ta bort.

1. Klicka på **[!UICONTROL Delete]**.

## Nästa steg {#next-steps}

* Ge produktfeedback med [!UICONTROL Feedback] alternativ som finns i användargränssnittet i resursvyn

* Ge feedback på dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som finns till höger

* Kontakt [Kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)
