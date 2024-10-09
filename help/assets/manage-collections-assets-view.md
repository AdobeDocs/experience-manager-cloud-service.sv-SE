---
title: Hantera samlingar
description: En samling är en uppsättning resurser i vyn Experience Manager Assets. Använd samlingar för att dela resurser mellan användare.
exl-id: 540dc1d9-eaf4-4e08-8087-dc58da23a6e8
feature: Collections, Asset Management
role: User
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Hantera samlingar {#manage-collections}

| [Sök efter bästa praxis](/help/assets/search-best-practices.md) | [Metadata - bästa praxis](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets-dokumentation för utvecklare](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!CONTEXTUALHELP]
>id="assets_collections"
>title="Hantera samlingar"
>abstract="En samling är en uppsättning resurser, mappar eller andra samlingar i vyn Assets. Använd samlingar för att dela resurser mellan användare. Till skillnad från mappar kan en samling innehålla resurser från olika platser. Du kan dela flera samlingar med en användare. Varje samling innehåller referenser till resurser. Resursernas referensintegritet bevaras i alla samlingar."

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

* [Hantera behörigheter till en privat samling](#manage-permissions-to-a-private-collection)

## Skapa en samling {#create-collection}

Så här skapar du en samling:

1. Klicka på **[!UICONTROL Collections]** i den vänstra listen och klicka sedan på **[!UICONTROL Create Collection]**.

1. Ange en rubrik och en valfri beskrivning för samlingen.

1. Välj om du behöver skapa en privat samling eller en offentlig samling. En offentlig samling är tillgänglig för visning och redigering av alla användare. En privat samling är dock tillgänglig för skaparen och användare med administratörsbehörighet.

1. Klicka på **[!UICONTROL Create]** för att skapa samlingen.

![Skapa samling](assets/create-collection.png)

<!--
   
   for viewing and editing only to users with the appropriate [permissions](#manage-collection-access).

-->

## Lägga till resurser i en samling {#add-assets-to-collection}

Så här lägger du till resurser i en samling:

1. Klicka på **[!UICONTROL Assets]** i den vänstra listen och välj de resurser som du vill lägga till i en samling.

1. Klicka på **[!UICONTROL Add to Collection]**.

1. I dialogrutan [!UICONTROL Collections] väljer du de samlingar som du vill lägga till de valda resurserna.

1. Klicka på **[!UICONTROL Add]** om du vill lägga till resursen i de valda samlingarna.

## Ta bort resurser från en samling {#remove-assets-from-collection}

Så här tar du bort resurser från en samling:

1. Klicka på **[!UICONTROL Collections]** i den vänstra listen för att visa listan över samlingar.

1. Klicka på samlingen och markera objekt som du vill ta bort från samlingen.

1. Klicka på **[!UICONTROL Remove]**.

## Hantera en smart samling {#manage-smart-collection}

Spara sökresultaten som en smart samling för att dynamiskt uppdatera samlingens innehåll. Om det finns resurser som har lagts till i Assets-vydatabasen och som passar de sökvillkor som angavs när du skapade den smarta samlingen, uppdateras innehållet i den smarta samlingen automatiskt när du öppnar en smart samling.

### Skapa en smart samling {#create-smart-collection}

Så här skapar du en smart samling:

1. Klicka på **[!UICONTROL Filter]** och [definiera sökvillkoren](search-assets-view.md#refine-search-results).

1. Klicka på **[!UICONTROL Save as]** och välj sedan **[!UICONTROL Smart Collection]**.

   ![Skapa smart samling](assets/create-smart-collection.png)

1. Ange en rubrik och en beskrivning för den smarta samlingen i dialogrutan [!UICONTROL Create Smart Collection].

1. Välj **[!UICONTROL Public Collection]** om du vill att alla användare ska kunna komma åt samlingen. Välj **[!UICONTROL Private Collection]** om du behöver en begränsad grupp användare för att komma åt samlingen.

1. Klicka på **[!UICONTROL Create]** för att skapa den smarta samlingen.

### Redigera en smart samling {#edit-smart-collection}

Så här redigerar du en smart samling:

1. Klicka på **[!UICONTROL Collections]** i den vänstra listen och dubbelklicka sedan på namnet på samlingen som du vill redigera.

1. Klicka på **[!UICONTROL Edit Smart Collection]**.

1. I dialogrutan [!UICONTROL Edit Smart Collection Filters] [uppdaterar du sökvillkoren](search-assets-view.md#refine-search-results) för den smarta samlingen.

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

1. Klicka på **[!UICONTROL Collections]** i den vänstra listen, markera en samling och klicka på **[!UICONTROL Details]**.
1. Visa samlingens metadata på fliken **[!UICONTROL Basic]**.
1. Ändra metadatafälten efter behov. Du kan ändra fälten [!UICONTROL Title] och [!UICONTROL Description].

![Samlingsmetadata](assets/collection-metadata.png)

## Dela länkar för samlingar {#share-collection-links}

Med [!DNL Assets view] kan du skapa en länk och dela samlingar och resurser i samlingar med externa intressenter som inte har tillgång till programmet [!DNL Assets view]. Du kan definiera ett förfallodatum för länken och sedan dela det med andra via den kommunikationsmetod du föredrar, som e-post eller meddelandetjänster. Mottagarna av länken kan förhandsgranska resurser och hämta dem.

![Dela länk för resurser](assets/share-link-collections.png)

Mer information om hur du delar samlingslänkar med externa intressenter finns i [Dela länkar för resurser](/help/assets/share-links-for-assets-view.md).

## Hämta en samling {#download-collection}

Så här hämtar du en samling:

1. Klicka på **[!UICONTROL Collections]** i den vänstra listen.

1. Välj den samling som du vill hämta och klicka på **[!UICONTROL Download]**.

1. Klicka på **[!UICONTROL OK]** i dialogrutan [!UICONTROL Downloading Asset].

Samlingen laddas ned som en ZIP-fil på den lokala datorn.

## Ta bort en samling {#delete-collection}

Så här tar du bort en samling:

1. Klicka på **[!UICONTROL Collections]** i den vänstra listen.

1. Markera den samling som du vill ta bort.

1. Klicka på **[!UICONTROL Delete]**.

## Hantera behörigheter för en privat samling{#manage-permissions-private-collection}

Du kan tillåta administratörer att hantera [åtkomstnivåer](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions) för privata samlingar som är tillgängliga i databasen. Du kan tilldela användargrupperna eller användarna behörigheter som `Can View` och `Can Edit`. Du kan även delegera behörighetshanteringsbehörigheter till användargrupper. De användare som skapar privata samlingar är ägare av dessa samlingar. De kan använda åtgärden [!UICONTROL Manage Permissions] för att bevilja åtkomst till de andra användarna. Administratörer kan dessutom visa och hantera behörigheter för de privata samlingarna i databasen [!DNL Experience Manager].
<!--
>[!NOTE]
>
>Adobe does not recommend to assign permissions to users.
-->
Mer information om hur du tilldelar tillgängliga behörigheter till användargrupper finns i [Lägga till behörigheter till användargrupper](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

Mer information om arbetsflödet från början till slut finns i [Hantera behörigheter](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions).

## Nästa steg {#next-steps}

* Ge produktfeedback med alternativet [!UICONTROL Feedback] som finns i användargränssnittet i Assets-vyn

* Ge feedback om dokumentationen med [!UICONTROL Edit this page] ![redigera sidan](assets/do-not-localize/edit-page.png) eller [!UICONTROL Log an issue] ![skapa ett GitHub-problem](assets/do-not-localize/github-issue.png) som är tillgängligt på den högra sidopanelen

* Kontakta [kundtjänst](https://experienceleague.adobe.com/?support-solution=General#support)
