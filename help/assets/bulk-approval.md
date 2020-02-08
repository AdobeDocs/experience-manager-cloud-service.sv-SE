---
title: Granska resurser i mappar och samlingar
description: Ställ in granskningsarbetsflöden för material i en mapp eller en samling och dela dem med granskare eller kreativa partners för att få feedback.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Granska resurser i mappar och samlingar {#review-folder-assets-and-collections}

Med Adobe Experience Manager Assets (AEM) kan ni skapa ad hoc-granskningsarbetsflöden för resurser som finns i en mapp eller i en samling. Du kan dela det med granskare eller kreativa partners för att få feedback. Du kan antingen associera ett granskningsarbetsflöde med ett projekt eller skapa en oberoende granskningsåtgärd.

När du har delat resurserna kan granskarna godkänna eller avvisa dem. Meddelanden skickas i olika faser av arbetsflödet för att meddela avsedda mottagare om att olika uppgifter har slutförts. När du till exempel delar en mapp eller samling får granskaren ett meddelande om att en mapp/samling har delats för granskning.

När granskaren har slutfört granskningen (godkänner eller avvisar resurser) får du ett meddelande om slutförd granskning.

## Skapa en granskningsåtgärd för mappar {#creating-a-review-task-for-folders}

1. I Assets-användargränssnittet väljer du den mapp som du vill skapa en granskningsuppgift för.
1. Tryck/klicka på ikonen **[!UICONTROL Skapa granskningsuppgift]** i verktygsfältet för att öppna sidan **[!UICONTROL Granskningsuppgift]** . Om du inte kan se ikonen i verktygsfältet trycker/klickar du på **[!UICONTROL Mer]** och väljer sedan ikonen.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Valfritt) I listan **[!UICONTROL Projekt]** väljer du det projekt som du vill associera granskningsaktiviteten med. Som standard är alternativet **[!UICONTROL Ingen]** markerat. Om du inte vill associera något projekt med granskningsaktiviteten ska du behålla det här valet.

   >[!NOTE]
   >
   >Endast de projekt som du har redigeringsbehörighet för (eller högre) visas i listan **[!UICONTROL Projekt]** .

1. Ange ett namn för granskningsaktiviteten och välj en godkännare i listan **[!UICONTROL Tilldela till]** .

   >[!NOTE]
   >
   >Medlemmarna/grupperna i det valda projektet är tillgängliga som godkännare i listan **[!UICONTROL Tilldela till]** .

1. Ange en beskrivning, uppgiftsprioritet och förfallodatum för granskningsaktiviteten.

   ![task_details](assets/task_details.png)

1. På fliken Avancerat anger du en etikett som ska användas för att skapa URI:n.

   ![review_name](assets/review_name.png)

1. Tryck/klicka på **[!UICONTROL Skicka]** och sedan på/klicka på **[!UICONTROL Klar]** för att stänga bekräftelsemeddelandet. Ett meddelande om den nya uppgiften skickas till godkännaren.
1. Logga in på AEM Assets som godkännare och navigera till Assets UI. Om du vill godkänna resurser klickar/trycker du på ikonen **[!UICONTROL Notifications]** (Meddelanden) och väljer sedan granskningsåtgärden i listan.

   ![meddelande](assets/notification.png)

1. Granska informationen om granskningsaktiviteten på sidan **[!UICONTROL Granska uppgift]** och tryck/klicka sedan på **[!UICONTROL Granska]**.
1. Markera resurser på sidan **[!UICONTROL Granska uppgift]** och tryck/klicka på ikonen **[!UICONTROL Godkänn/Avvisa]** för att godkänna eller avvisa.

   ![review_task](assets/review_task.png)

1. Tryck/klicka på ikonen **[!UICONTROL Slutför]** i verktygsfältet. Skriv en kommentar i dialogrutan och bekräfta genom att trycka/klicka på **[!UICONTROL Slutför]** .
1. Navigera till resursgränssnittet och öppna mappen. Ikonerna för godkännandestatus för resurserna visas både i kort- och listvyn.

   **Kortvy**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **Listvy**

   ![review_status_listview](assets/review_status_listview.png)

## Skapa en granskningsuppgift för samlingar {#creating-a-review-task-for-collections}

1. På sidan Samlingar väljer du den samling som du vill skapa en granskningsuppgift för.
1. Tryck/klicka på ikonen **[!UICONTROL Skapa granskningsuppgift]** i verktygsfältet för att öppna sidan **[!UICONTROL Granskningsuppgift]** . Om du inte kan se ikonen i verktygsfältet trycker/klickar du på **[!UICONTROL Mer]** och väljer sedan ikonen.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Valfritt) I listan **[!UICONTROL Projekt]** väljer du det projekt som du vill associera granskningsaktiviteten med. Som standard är alternativet **[!UICONTROL Ingen]** markerat. Om du inte vill associera något projekt med granskningsaktiviteten ska du behålla det här valet.

   >[!NOTE]
   >
   >Endast de projekt som du har redigeringsbehörighet för (eller högre) visas i listan **[!UICONTROL Projekt]** .

1. Ange ett namn för granskningsaktiviteten och välj en godkännare i listan **[!UICONTROL Tilldela till]** .

   >[!NOTE]
   >
   >Medlemmarna/grupperna i det valda projektet är tillgängliga som godkännare i listan **[!UICONTROL Tilldela till]** .

1. Ange en beskrivning, uppgiftsprioritet och förfallodatum för granskningsaktiviteten.

   ![task_details-collection](assets/task_details-collection.png)

1. Tryck/klicka på **[!UICONTROL Skicka]** och sedan på/klicka på **[!UICONTROL Klar]** för att stänga bekräftelsemeddelandet. Ett meddelande om den nya uppgiften skickas till godkännaren.
1. Logga in på AEM Assets som godkännare och navigera till Assets-konsolen. Om du vill godkänna resurser trycker/klickar du på **[!UICONTROL meddelandeikonen]** och väljer sedan granskningsåtgärden i listan.
1. Granska informationen om granskningsaktiviteten på sidan **[!UICONTROL Granska uppgift]** och tryck/klicka sedan på **[!UICONTROL Granska]**.
1. Alla resurser i samlingen visas på granskningssidan. Markera resurserna och tryck/klicka på ikonen **[!UICONTROL Godkänn/Avvisa]** för att godkänna eller avvisa resurser.

   ![review_task_collection](assets/review_task_collection.png)

1. Tryck/klicka på ikonen **[!UICONTROL Slutför]** i verktygsfältet. Skriv en kommentar i dialogrutan och bekräfta genom att trycka/klicka på **[!UICONTROL Slutför]** .
1. Navigera till samlingskonsolen och öppna samlingen. Ikonerna för godkännandestatus för resurserna visas både i kort- och listvyn.

   **Kortvy**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **Listvy**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

