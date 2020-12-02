---
title: Checka in och checka ut filer i [!DNL Assets]
description: Lär dig hur du checkar ut resurser för redigering och checkar in dem igen när ändringarna är klara.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 6%

---


# Checka in och checka ut filer i Assets {#check-in-and-check-out-files-in-assets}

Med Adobe Experience Manager (AEM) Assets kan du checka ut resurser för redigering och checka in dem igen när du är klar med ändringarna. När du har checkat ut en resurs kan bara du redigera, kommentera, publicera, flytta eller ta bort resursen. När du checkar ut en resurs låses den. Andra användare kan inte utföra någon av dessa åtgärder på resursen förrän du checkar in resursen på AEM Assets igen. De kan dock fortfarande ändra metadata för den låsta resursen.

Om du vill kunna checka ut/in resurser måste du ha skrivbehörighet för dem.

Den här funktionen förhindrar att andra användare åsidosätter ändringar som gjorts av en författare där flera användare samarbetar i redigeringsarbetsflöden mellan team.

## Checkar ut resurser {#checking-out-assets}

1. I resursgränssnittet väljer du den resurs du vill checka ut. Du kan också välja flera resurser att checka ut.

   ![chlimage_1-468](assets/chlimage_1-468.png)

1. Klicka/tryck på ikonen **[!UICONTROL Checkout]** i verktygsfältet.

   ![chlimage_1-469](assets/chlimage_1-469.png)

   Observera att ikonen **[!UICONTROL Checkout]** växlar till ikonen **[!UICONTROL Checkin]** när låset är öppet.

   ![chlimage_1-470](assets/chlimage_1-470.png)

   Logga in som en annan användare om du vill kontrollera om andra användare kan redigera den utcheckade resursen. En låsikon visas på miniatyrbilden för resursen som du har checkat ut.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Markera resursen. Observera att verktygsfältet inte visar några alternativ som gör att du kan redigera, kommentera, publicera eller ta bort resursen.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Du kan emellertid klicka/trycka på ikonen **[!UICONTROL View Properties]** för att redigera metadata för den låsta resursen.

1. Klicka på/tryck på ikonen Redigera för att öppna resursen i redigeringsläge.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Redigera resursen och spara ändringarna. Beskär till exempel bilden och spara.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Du kan också välja att anteckna eller publicera resursen.

1. Välj den redigerade resursen i Assets-gränssnittet och klicka/tryck på ikonen **[!UICONTROL Checkin]** i verktygsfältet.

   ![chlimage_1-475](assets/chlimage_1-475.png)

   Den ändrade resursen checkas in i AEM Assets och är tillgänglig för andra användare för redigering.

## Tvingad incheckning {#forced-check-in}

Administratörer kan checka in resurser som är utcheckade av andra användare.

1. Logga in på AEM Assets som administratör.
1. I resursgränssnittet väljer du en eller flera resurser som har checkats ut av andra användare.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Klicka/tryck på ikonen **[!UICONTROL Release Lock]** i verktygsfältet. Resursen checkas in igen och är tillgänglig för redigering för andra användare.

   ![chlimage_1-477](assets/chlimage_1-477.png)