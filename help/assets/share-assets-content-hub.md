---
title: Dela Assets i [!DNL the Content Hub]
description: Dela Assets i [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Dela resurser i Content Hub {#search-assets-as-a-link}

Skapa en länk till valda resurser för att enkelt dela dem med andra. Som auktoriserad [!DNL Content Hub]-användare väljer du en eller flera resurser som är tillgängliga i din [!DNL Content Hub]-miljö, skapar en länk och skickar den till andra privata eller offentliga användare.

## Förutsättningar {#prerequisites}

[Content Hub-användare](deploy-content-hub.md#onboard-content-hub-users) kan skapa en länk till markerade resurser och dela den med andra användare.

## Dela resurser {#share-assets}

Så här delar du en eller flera resurser med privata eller offentliga användare:
1. Navigera till din [!DNL Content Hub]-hemsida, markera en eller flera resurser och klicka på ![ dela ](/help/assets/assets/share.svg) **[!UICONTROL Share]** för att visa en enskild markerad resurs eller en lista med flera markerade resurser i dialogrutan **[!UICONTROL Share assets]** .
Du kan också markera och dela resurser som är tillgängliga i ![samlingar](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL Collections]**.
1. Visa en resurs eller granska listan över tillgängliga resurser i dialogrutan **[!UICONTROL Share assets]**. Klicka på ![avmarkera](/help/assets/assets/Close.svg) bredvid en resurs för att avmarkera den i listan.
1. Välj en **[!UICONTROL period of expiration]** och klicka på **[!UICONTROL Generate Private Link]** för att skapa en länk som du kan dela med privata användare. Privata användare loggar in i sin [!DNL Content Hub]-miljö för att komma åt sidan med delade resurser.
   ![privat och offentlig länk](/help/assets/assets/private-and-public-link.png)
Aktivera växlingsknappen **[!UICONTROL Public Link]** , välj en **[!UICONTROL period of expiration]** och klicka på **[!UICONTROL Generate Public Link]** för att skapa en länk som ska delas med publika användare. Offentliga användare, som gäster, har åtkomst till sidan med delade resurser utan att logga in på [!DNL Content Hub].
   ![privat och offentlig länk](/help/assets/assets/public-and-private-link.png)

   >[!NOTE]
   > 
   > [Aktivera delning av offentlig länk från konfigurationssidan](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing) om du vill visa **[!UICONTROL Public Link]**-växlingen i dialogrutan **[!UICONTROL Share assets]**.

## Dela en resurs från dess förhandsgranskningssida {#share-asset-from-preview-page}

Utför följande steg för att dela en resurs när du förhandsgranskar den:

1. Navigera till startsidan för [!DNL Content Hub] och klicka på miniatyrbilden för resursen för att förhandsgranska resursen och visa menyalternativen till höger i dialogrutan.
1. Välj ![dela](/help/assets/assets/share.svg) om du vill visa panelen **[!UICONTROL Share]**.
   ![dela resurs vid förhandsgranskning](/help/assets/assets/share-assets-from-share-panel.png)
1. Följ steg 3 i avsnittet [Dela resurser](#share-assets) för att generera och dela resurslänken (privat eller offentlig) från den här **[!UICONTROL Share]**-panelen.

## Åtkomst till delade resurser {#access-shared-assets}

Gå till sidan med delade resurser via länken och gör följande:

* Välj en eller flera resurser och klicka på ![download](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]** för att välja **[!UICONTROL Original]**, **[!UICONTROL Static]** eller båda återgivningarna från de tillgängliga hämtningsalternativen.
  ![](/help/assets/assets/download-shared-assets.png)
* Klicka på miniatyrbilden för resursen för att visa resursens metadata.
* På sidan med delade resurser ([som nås via en privat länk](#share-assets)) klickar du på en miniatyrbild för resursen och väljer ![hämta](/help/assets/assets/download-icon.svg) för att markera och visa tillgängliga dynamiska återgivningar av resursen på panelen **[!UICONTROL Download]** innan du markerar och hämtar dem.
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)





