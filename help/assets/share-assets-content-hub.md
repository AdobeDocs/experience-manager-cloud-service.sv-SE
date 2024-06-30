---
title: Dela Assets i [!DNL the Content Hub]
description: Dela Assets i [!DNL the Content Hub]
role: User
source-git-commit: 5a968440c8841abe7af2c81c4af12258b7e4547f
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Dela resurser i Content Hub {#search-assets-as-a-link}

![Dela resurser - bannerbild](assets/share-assets-banner.png)

Att dela resurser via en länk är ett bekvämt sätt att göra resurserna tillgängliga för [!DNL the Content Hub] -användare. Funktionen gör att behöriga användare kan komma åt och hämta de resurser som delas med dem. När du hämtar resurser från en delad länk, [!DNL the Content Hub] använder en asynkron tjänst som ger snabbare och oavbruten nedladdning.

## Förutsättningar {#prerequisites}

[Content Hub](deploy-content-hub.md#onboard-content-hub-users) kan utföra åtgärder som nämns i den här artikeln.

## Dela en enda resurs {#share-a-single-asset}

Du kan dela en enskild resurs genom att utföra följande steg:

1. Välj en resurs och klicka på ![dela, ikon](assets/share.svg) om du vill dela en resurs.

   ![Dela en resurs](assets/sharing-single-asset.png)

1. Använd **[!UICONTROL Expiration]** för att ange ett förfallodatum för länken. Välj ett av de tillgängliga alternativen, till exempel 24 timmar, 1 vecka, 30 dagar, 90 dagar, 1 år eller ange ett anpassat datum.

1. Klicka på **[!UICONTROL Copy share link]**. Sedan kan du dela den kopierade länken med mottagaren.

## Dela flera resurser {#share-multiple-assets}

[!DNL The Content Hub] kan du dela flera resurser via en delad länk. Utför följande steg:

1. Välj resurser som du vill dela med den auktoriserade mottagaren. Du kan välja flera resurser en i taget eller klicka på **[!UICONTROL Select All]** om du vill välja alla tillgängliga resurser på en gång. The **[!UICONTROL Select All]** visas bara när du väljer minst en resurs.

1. Klicka på ![dela, ikon](assets/share.svg) -ikon.

   ![Dela flera resurser](assets/sharing-multiple-assets.png)

1. I förhandsvisningsavsnittet kan du även ta bort resurser efter dina behov. Använd **[!UICONTROL Expiration]** för att ange ett förfallodatum för länken. Välj ett av de tillgängliga alternativen, till exempel 24 timmar, 1 vecka, 30 dagar, 90 dagar, 1 år eller ange ett anpassat datum.

1. Klicka på **[!UICONTROL Copy share link]**. Sedan kan du dela den kopierade länken med mottagaren.

## Förhandsgranska och dela resurser {#preview-assets}

Du kan förhandsgranska om du vill se hur en digital resurs ser ut innan du delar den med en länkmottagare. Klicka på resursen som du vill förhandsgranska. The [!DNL Content Hub] visar [detaljerad vy för resursen](asset-properties-content-hub.md).

Klicka på ![dela, ikon](assets/share.svg) om du vill dela en resurs. Använd **[!UICONTROL Expiration]** för att ange ett förfallodatum för länken. Välj ett av de tillgängliga alternativen, till exempel 24 timmar, 1 vecka, 30 dagar, 90 dagar, 1 år eller ange ett anpassat datum. Klicka på **[!UICONTROL Copy share link]**. Sedan kan du dela den kopierade länken med mottagaren.

![Förhandsgranska resurser i Content Hub](assets/preview-assets-content-hub.png)

## Åtkomst till delade resurser {#access-shared-assets}

När länken för resurserna har delats kan de behöriga mottagarna klicka på länken för att förhandsgranska eller hämta de delade resurserna i en webbläsare.

Klicka på den delade länken och klicka på nedladdningsikonen som finns på resurskortet för att hämta en resurs.  Du kan också markera flera resurser och klicka på **[!UICONTROL Download]**. <!--You can either download original assets or Original+Renditions of an asset.--> [!DNL The Content Hub] hämtar varje resurs en i taget till det lokala filsystemet.

![Använd delade länkar](assets/content-hub-access-shared-links.png)




