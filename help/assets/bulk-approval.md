---
title: Granska resurser i mappar och samlingar
description: Ställ in granskningsarbetsflöden för material i en mapp eller en samling och dela dem med granskare eller kreativa partners för att få feedback.
contentOwner: AG
feature: Collections, Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 4%

---

# Granska resurser i mappar och samlingar {#review-folder-assets-and-collections}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

Med Adobe Experience Manager Assets kan du ange ad hoc-granskningsarbetsflöden för resurser som finns i en mapp eller i en samling. Du kan dela det med granskare eller kreativa partners för att få feedback. Du kan antingen associera ett granskningsarbetsflöde med ett projekt eller skapa en oberoende granskningsåtgärd.

När du har delat resurserna kan granskarna godkänna eller avvisa dem. Meddelanden skickas i olika faser av arbetsflödet för att meddela avsedda mottagare om att olika uppgifter har slutförts. När du till exempel delar en mapp eller samling får granskaren ett meddelande om att en mapp/samling har delats för granskning.

När granskaren har slutfört granskningen (godkänner eller avvisar resurser) får du ett meddelande om slutförd granskning.

## Skapa en granskningsåtgärd för mappar {#creating-a-review-task-for-folders}

1. I Assets-användargränssnittet väljer du den mapp som du vill skapa en granskningsåtgärd för.
1. I verktygsfältet väljer du ikonen **[!UICONTROL Create Review Task]** för att öppna sidan **[!UICONTROL Review Task]**. Om du inte kan se ikonen i verktygsfältet väljer du **[!UICONTROL More]** och sedan ikonen.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Valfritt) I listan **[!UICONTROL Project]** väljer du det projekt som du vill associera granskningsaktiviteten med. Som standard är alternativet **[!UICONTROL None]** markerat. Om du inte vill associera något projekt med granskningsaktiviteten ska du behålla det här valet.

   >[!NOTE]
   >
   >Endast de projekt som du har redigeringsbehörighet för (eller högre) visas i listan **[!UICONTROL Projects]**.

1. Ange ett namn för granskningsaktiviteten och välj en godkännare i listan **[!UICONTROL Assign To]**.

   >[!NOTE]
   >
   >Medlemmarna/grupperna i det valda projektet är tillgängliga som godkännare i listan **[!UICONTROL Assign To]**.

1. Ange en beskrivning, uppgiftsprioritet och förfallodatum för granskningsaktiviteten.

   ![task_details](assets/task_details.png)

1. Ange en etikett som ska användas för att skapa URI på fliken Avancerat.

   ![review_name](assets/review_name.png)

1. Välj **[!UICONTROL Submit]** och välj sedan **[!UICONTROL Done]** för att stänga bekräftelsemeddelandet. Ett meddelande om den nya uppgiften skickas till godkännaren.
1. Logga in på [!DNL Experience Manager Assets] som godkännare och navigera till användargränssnittet i Assets. Om du vill godkänna resurser väljer du ikonen **[!UICONTROL Notifications]** och sedan granskningsaktiviteten i listan.

   ![meddelande](assets/notification.png)

1. Granska informationen om granskningsaktiviteten på sidan **[!UICONTROL Review Task]** och välj sedan **[!UICONTROL Review]**.
1. Markera resurser på sidan **[!UICONTROL Review Task]** och välj ikonen **[!UICONTROL Approve/Reject]** för att godkänna eller avvisa, beroende på vad som är lämpligt.

   ![review_task](assets/review_task.png)

1. Välj ikonen **[!UICONTROL Complete]** i verktygsfältet. Skriv en kommentar i dialogrutan och välj **[!UICONTROL Complete]** för att bekräfta.
1. Navigera till Assets-gränssnittet och öppna mappen. Ikonerna för godkännandestatus för resurserna visas både i kort- och listvyn.

   **Kortvy**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **Listvy**

   ![review_status_listview](assets/review_status_listview.png)

## Skapa en granskningsuppgift för samlingar {#creating-a-review-task-for-collections}

1. På sidan Samlingar väljer du den samling som du vill skapa en granskningsuppgift för.
1. I verktygsfältet väljer du ikonen **[!UICONTROL Create Review Task]** för att öppna sidan **[!UICONTROL Review Task]**. Om du inte kan se ikonen i verktygsfältet väljer du **[!UICONTROL More]** och sedan ikonen.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Valfritt) I listan **[!UICONTROL Project]** väljer du det projekt som du vill associera granskningsaktiviteten med. Som standard är alternativet **[!UICONTROL None]** markerat. Om du inte vill associera något projekt med granskningsaktiviteten ska du behålla det här valet.

   >[!NOTE]
   >
   >Endast de projekt som du har redigeringsbehörighet för (eller högre) visas i listan **[!UICONTROL Projects]**.

1. Ange ett namn för granskningsaktiviteten och välj en godkännare i listan **[!UICONTROL Assign To]**.

   >[!NOTE]
   >
   >Medlemmarna/grupperna i det valda projektet är tillgängliga som godkännare i listan **[!UICONTROL Assign To]**.

1. Ange en beskrivning, uppgiftsprioritet och förfallodatum för granskningsaktiviteten.

   ![task_details-collection](assets/task_details-collection.png)

1. Välj **[!UICONTROL Submit]** och välj sedan **[!UICONTROL Done]** för att stänga bekräftelsemeddelandet. Ett meddelande om den nya uppgiften skickas till godkännaren.
1. Logga in på [!DNL Experience Manager Assets] som godkännare och navigera till Assets-konsolen. Om du vill godkänna resurser väljer du ikonen **[!UICONTROL Notifications]** och sedan granskningsaktiviteten i listan.
1. Granska informationen om granskningsaktiviteten på sidan **[!UICONTROL Review Task]** och välj sedan **[!UICONTROL Review]**.
1. Alla resurser i samlingen visas på granskningssidan. Markera resurserna och välj ikonen **[!UICONTROL Approve/Reject]** om du vill godkänna eller avvisa resurserna.

   ![review_task_collection](assets/review_task_collection.png)

1. Välj ikonen **[!UICONTROL Complete]** i verktygsfältet. Skriv en kommentar i dialogrutan och välj **[!UICONTROL Complete]** för att bekräfta.
1. Navigera till samlingskonsolen och öppna samlingen. Ikonerna för godkännandestatus för resurserna visas både i kort- och listvyn.

   **Kortvy**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **Listvy**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
