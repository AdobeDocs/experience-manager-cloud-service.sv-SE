---
title: Checka in och checka ut filer i [!DNL Assets]
description: Lär dig hur du checkar ut resurser för redigering och checkar in dem igen när ändringarna är klara.
contentOwner: AG
feature: Asset Management
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 2%

---


# Checka in och checka ut filer i [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] Med kan du checka ut resurser för redigering och checka in dem igen när du har gjort ändringarna. När du har checkat ut en resurs kan bara du redigera, kommentera, publicera, flytta eller ta bort resursen. När du checkar ut en resurs låses den. Andra användare kan inte utföra någon av dessa åtgärder på resursen förrän du checkar in resursen igen på [!DNL Assets]. De kan dock fortfarande ändra metadata för den låsta resursen.

Om du vill kunna checka ut/in resurser måste du ha skrivbehörighet för dem.

Den här funktionen förhindrar att andra användare åsidosätter ändringar som gjorts av en författare där flera användare samarbetar i redigeringsarbetsflöden mellan team.

## Kolla in resurser {#checking-out-assets}

1. Välj den resurs du vill checka ut i [!DNL Assets]-användargränssnittet. Du kan också välja flera resurser att checka ut.

1. Klicka på **[!UICONTROL Checkout]** i verktygsfältet. Alternativet **[!UICONTROL Checkout]** växlar till **[!UICONTROL Checkin]**.
Logga in som en annan användare om du vill kontrollera om andra användare kan redigera den utcheckade resursen. Ikonen ![ikonen för utcheckningslås](assets/do-not-localize/checkout_lock.png) visas på miniatyrbilden för den resurs som du har checkat ut.

   ![utcheckningsikon i kortvyn](assets/checkout-icon-card-view.png)

   Markera resursen. Observera att verktygsfältet inte visar några alternativ som gör att du kan redigera, kommentera, publicera eller ta bort resursen.

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   Om du vill redigera metadata för den låsta resursen klickar du på **[!UICONTROL View Properties]**.

1. Klicka på **[!UICONTROL Edit]** för att öppna resursen i redigeringsläge.

1. Redigera resursen och spara ändringarna. Beskär till exempel bilden och spara. Du kan också välja att anteckna eller publicera resursen.

1. Välj den redigerade resursen i gränssnittet [!DNL Assets] och klicka på **[!UICONTROL Checkin]** i verktygsfältet. Den ändrade resursen checkas in i [!DNL Assets] och är tillgänglig för andra användare för redigering.

## Tvingad incheckning {#forced-check-in}

Administratörer kan checka in resurser som är utcheckade av andra användare.

1. Logga in på [!DNL Assets] som administratör.
1. I [!DNL Assets]-användargränssnittet väljer du en eller flera resurser som har checkats ut av andra användare.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Klicka på **[!UICONTROL Release Lock]** i verktygsfältet. Resursen checkas in igen och är tillgänglig för redigering för andra användare.

## God praxis och begränsningar {#tips-limitations}

* Det går att ta bort en *mapp* som innehåller utcheckade resursfiler. Innan du tar bort en mapp kontrollerar du att inga digitala resurser är utcheckade av användarna.

>[!MORELIKETHIS]
>
>* [Förstå in- och utcheckning av  [!DNL Experience Manager] sktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [Videosjälvstudiekurs för att förstå hur du checkar in och checkar ut [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

