---
title: Checka in och checka ut filer i [!DNL Assets]
description: Lär dig hur du checkar ut resurser för redigering och checkar in dem igen när ändringarna är klara.
contentOwner: AG
feature: Asset Management
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: 034899c2a717fafdc50cc269d6db3feb77d907c5
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 2%

---

# Checka in och checka ut filer i [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] Med kan du checka ut resurser för redigering och checka in dem igen när du har gjort ändringarna. När du har checkat ut en resurs kan bara du redigera, kommentera, publicera, flytta eller ta bort resursen. När du checkar ut en resurs låses den. Andra användare kan inte utföra någon av dessa åtgärder på resursen förrän du checkar in resursen igen på [!DNL Assets]. However, they can still change the metadata for the locked asset.

To be able to check out/in assets, you require Write access on them.

This feature helps prevent other users from overriding the changes made by an author where multiple users collaborate on editing workflows across teams.

## Check out assets {#checking-out-assets}

1. Från [!DNL Assets] väljer du den resurs du vill checka ut i användargränssnittet. Du kan också välja flera resurser att checka ut.

1. Klicka på **[!UICONTROL Checkout]** i verktygsfältet. The **[!UICONTROL Checkout]** alternativ växlar till **[!UICONTROL Checkin]**.
Logga in som en annan användare om du vill kontrollera om andra användare kan redigera den utcheckade resursen. Ikonen ![låsikon för utcheckning](assets/do-not-localize/checkout_lock.png) visas på miniatyrbilden för den resurs som du har checkat ut.

   ![utcheckningsikon i kortvyn](assets/checkout-icon-card-view.png)

   Select the asset. Observera att verktygsfältet inte visar några alternativ som gör att du kan redigera, kommentera, publicera eller ta bort resursen.

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   Om du vill redigera metadata för den låsta resursen klickar du på **[!UICONTROL View Properties]**.

1. Click **[!UICONTROL Edit]** to open the asset in edit mode.

1. Edit the asset and save the changes. Beskär till exempel bilden och spara. You can also choose to annotate or publish the asset.

1. Select the edited asset from the [!DNL Assets] interface, and click **[!UICONTROL Checkin]** from the toolbar. The modified asset is checked in to [!DNL Assets] and is available to other users for editing.

## Tvingad incheckning {#forced-check-in}

Administratörer kan checka in resurser som är utcheckade av andra användare.

1. Logga in på [!DNL Assets] som administratör.
1. Från [!DNL Assets] användargränssnittet väljer en eller flera resurser som har checkats ut av andra användare.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Klicka på **[!UICONTROL Release Lock]** i verktygsfältet. The asset is checked back in and available for edit to other users.

## Best practices and limitations {#tips-limitations}

* Du kan ta bort en *mapp* som innehåller utcheckade resursfiler. Innan du tar bort en mapp kontrollerar du att inga digitala resurser är utcheckade av användarna.

>[!MORELIKETHIS]
>
>* [Förstå in- och utcheckning [!DNL Experience Manager] datorprogram](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Videosjälvstudiekurs för att förstå hur du checkar in och checkar ut [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

