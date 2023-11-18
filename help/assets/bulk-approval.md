---
title: Granska resurser i mappar och samlingar
description: Ställ in granskningsarbetsflöden för material i en mapp eller en samling och dela dem med granskare eller kreativa partners för att få feedback.
contentOwner: AG
feature: Collections,Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 5%

---

# Granska resurser i mappar och samlingar {#review-folder-assets-and-collections}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Med Adobe Experience Manager Assets kan du ange ad hoc-granskningsarbetsflöden för resurser som finns i en mapp eller i en samling. Du kan dela det med granskare eller kreativa partners för att få feedback. Du kan antingen associera ett granskningsarbetsflöde med ett projekt eller skapa en oberoende granskningsåtgärd.

När du har delat resurserna kan granskarna godkänna eller avvisa dem. Meddelanden skickas i olika faser av arbetsflödet för att meddela avsedda mottagare om att olika uppgifter har slutförts. När du till exempel delar en mapp eller samling får granskaren ett meddelande om att en mapp/samling har delats för granskning.

När granskaren har slutfört granskningen (godkänner eller avvisar resurser) får du ett meddelande om slutförd granskning.

## Skapa en granskningsåtgärd för mappar {#creating-a-review-task-for-folders}

1. I Assets-användargränssnittet väljer du den mapp som du vill skapa en granskningsuppgift för.
1. Välj **[!UICONTROL Create Review Task]** -ikonen för att öppna **[!UICONTROL Review Task]** sida. Om ikonen inte visas i verktygsfältet väljer du **[!UICONTROL More]** och sedan markera ikonen.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Valfritt) Från **[!UICONTROL Project]** väljer du det projekt som du vill associera granskningsuppgiften med. Som standard är **[!UICONTROL None]** är markerat. Om du inte vill associera något projekt med granskningsaktiviteten ska du behålla det här valet.

   >[!NOTE]
   >
   >Endast de projekt som du har redigerarbehörighet för (eller högre) visas i **[!UICONTROL Projects]** lista.

1. Ange ett namn för granskningsaktiviteten och välj en godkännare på menyn **[!UICONTROL Assign To]** lista.

   >[!NOTE]
   >
   >Medlemmarna/grupperna i det valda projektet är tillgängliga som godkännare i **[!UICONTROL Assign To]** lista.

1. Ange en beskrivning, uppgiftsprioritet och förfallodatum för granskningsaktiviteten.

   ![task_details](assets/task_details.png)

1. Ange en etikett som ska användas för att skapa URI på fliken Avancerat.

   ![review_name](assets/review_name.png)

1. Välj **[!UICONTROL Submit]** och sedan markera **[!UICONTROL Done]** för att stänga bekräftelsemeddelandet. Ett meddelande om den nya uppgiften skickas till godkännaren.
1. Logga in på [!DNL Experience Manager Assets] som godkännare och navigera till resursgränssnittet. Om du vill godkänna resurser väljer du **[!UICONTROL Notifications]** och välj sedan en granskningsåtgärd i listan.

   ![meddelande](assets/notification.png)

1. I **[!UICONTROL Review Task]** Granska informationen om granskningsaktiviteten och välj **[!UICONTROL Review]**.
1. I **[!UICONTROL Review Task]** väljer du resurser och väljer **[!UICONTROL Approve/Reject]** ikon för att godkänna eller avvisa, beroende på vad som är lämpligt.

   ![review_task](assets/review_task.png)

1. Välj **[!UICONTROL Complete]** -ikonen i verktygsfältet. Skriv en kommentar i dialogrutan och välj  **[!UICONTROL Complete]** för att bekräfta.
1. Navigera till resursgränssnittet och öppna mappen. Ikonerna för godkännandestatus för resurserna visas både i kort- och listvyn.

   **Kortvy**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **Listvy**

   ![review_status_listview](assets/review_status_listview.png)

## Skapa en granskningsuppgift för samlingar {#creating-a-review-task-for-collections}

1. På sidan Samlingar väljer du den samling som du vill skapa en granskningsuppgift för.
1. Välj **[!UICONTROL Create Review Task]** -ikonen för att öppna **[!UICONTROL Review Task]** sida. Om ikonen inte visas i verktygsfältet väljer du **[!UICONTROL More]** och sedan markera ikonen.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Valfritt) Från **[!UICONTROL Project]** väljer du det projekt som du vill associera granskningsuppgiften med. Som standard är **[!UICONTROL None]** är markerat. Om du inte vill associera något projekt med granskningsaktiviteten ska du behålla det här valet.

   >[!NOTE]
   >
   >Endast de projekt som du har redigerarbehörighet för (eller högre) visas i **[!UICONTROL Projects]** lista.

1. Ange ett namn för granskningsaktiviteten och välj en godkännare på menyn **[!UICONTROL Assign To]** lista.

   >[!NOTE]
   >
   >Medlemmarna/grupperna i det valda projektet är tillgängliga som godkännare i **[!UICONTROL Assign To]** lista.

1. Ange en beskrivning, uppgiftsprioritet och förfallodatum för granskningsaktiviteten.

   ![task_details-collection](assets/task_details-collection.png)

1. Välj **[!UICONTROL Submit]** och sedan markera **[!UICONTROL Done]** för att stänga bekräftelsemeddelandet. Ett meddelande om den nya uppgiften skickas till godkännaren.
1. Logga in på [!DNL Experience Manager Assets] som godkännare och navigera till Assets-konsolen. Om du vill godkänna resurser väljer du **[!UICONTROL Notifications]** och välj sedan en granskningsåtgärd i listan.
1. I **[!UICONTROL Review Task]** Granska informationen om granskningsaktiviteten och välj **[!UICONTROL Review]**.
1. Alla resurser i samlingen visas på granskningssidan. Markera resurserna och välj **[!UICONTROL Approve/Reject]** ikon för att godkänna eller avvisa resurser, beroende på vad som är lämpligt.

   ![review_task_collection](assets/review_task_collection.png)

1. Välj **[!UICONTROL Complete]** -ikonen i verktygsfältet. Skriv en kommentar i dialogrutan och välj **[!UICONTROL Complete]** för att bekräfta.
1. Navigera till samlingskonsolen och öppna samlingen. Ikonerna för godkännandestatus för resurserna visas både i kort- och listvyn.

   **Kortvy**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **Listvy**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

**Se även**

* [Översätt resurser](translate-assets.md)
* [HTTP API för Assets](mac-api-assets.md)
* [Resurser som stöds i filformat](file-format-support.md)
* [Söka efter resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Materialrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Söka efter fasetter](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
