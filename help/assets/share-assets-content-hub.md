---
title: Dela Assets i [!DNL the Content Hub]
description: Dela Assets i [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: a6d995eddd714c356eadc6c1b668887bdfd011cd
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Dela resurser i Content Hub {#search-assets-as-a-link}

Skapa en länk till valda resurser för att enkelt dela dem med andra. Som auktoriserad [!DNL Content Hub]-användare väljer du en eller flera resurser som är tillgängliga i din [!DNL Content Hub]-miljö, skapar en länk och skickar den till andra privata eller offentliga användare.

## Förutsättningar {#prerequisites}

[Content Hub-användare](deploy-content-hub.md#onboard-content-hub-users) kan skapa en länk till markerade resurser och dela den med andra användare.

## Dela resurser {#share-assets}

Så här delar du en eller flera resurser med privata eller offentliga användare:

1. Navigera till din [!DNL Content Hub]-hemsida, markera en eller flera resurser och klicka på ![&#x200B; dela &#x200B;](/help/assets/assets/share.svg) **[!UICONTROL Share]** för att visa en enskild markerad resurs eller en lista med flera markerade resurser i dialogrutan **[!UICONTROL Share assets]** .

   Du kan också markera och dela resurser som är tillgängliga i ![samlingar](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL Collections]**.

1. Visa en resurs eller granska listan över tillgängliga resurser i dialogrutan **[!UICONTROL Share assets]**. Klicka på ![avmarkera](/help/assets/assets/Close.svg) bredvid en resurs för att ta bort den från listan.

1. Ange en titel och en valfri beskrivning som definierar uppsättningen med valda resurser.

1. Välj **[!UICONTROL Period of expiration]**.

1. Under listrutan **[!UICONTROL Who can access]** väljer du åtkomstalternativen och klickar på **[!UICONTROL Get Link]** för att skapa en länk som du kan dela med de valda användarna. Privata användare måste logga in i sin [!DNL Content Hub]-miljö för att komma åt sidan med delade resurser. Offentliga användare, som gäster, har åtkomst till sidan med delade resurser utan att logga in på [!DNL Content Hub].

<!--1. Select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Get Link]** to generate a link to share with private users. Private users sign in to their [!DNL Content Hub] environment to access the shared assets page.-->

![privat och offentlig länk](/help/assets/assets/shared-link-for-assets.png)

<!--Enable the **[!UICONTROL Public Link]** toggle, select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Generate Public Link]** to generate a link to share with public users. Public users, as guests, access the shared assets page without signing in to [!DNL Content Hub].-->

>[!NOTE]
> 
> [Aktivera delning av offentlig länk från konfigurationssidan](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing) om du vill visa **[!UICONTROL Public Link]**-växlingen i dialogrutan **[!UICONTROL Share assets]**.

## Dela en resurs från dess förhandsgranskningssida {#share-asset-from-preview-page}

Utför följande steg för att dela en resurs när du förhandsgranskar den:

1. Navigera till startsidan för [!DNL Content Hub] och klicka på miniatyrbilden för resursen för att förhandsgranska resursen och visa menyalternativen till höger i dialogrutan.
1. Välj ![dela](/help/assets/assets/share.svg) om du vill visa panelen **[!UICONTROL Share]**.
   ![dela resurs vid förhandsgranskning](/help/assets/assets/share-link-asset-preview.png)
1. Följ steg 3 till 5 i avsnittet [Dela resurser](#share-assets) för att generera och dela resurslänken (privat eller offentlig) från den här **[!UICONTROL Share]** panelen.

## Åtkomst till delade resurser {#access-shared-assets}

Gå till sidan med delade resurser via länken och gör följande:

* Välj en eller flera resurser och klicka på ![download](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]** för att välja **[!UICONTROL Original]**, **[!UICONTROL Static]** eller båda återgivningarna från de tillgängliga hämtningsalternativen.
  ![](/help/assets/assets/download-shared-assets.png)
* Klicka på miniatyrbilden för resursen för att visa resursens metadata.
* På sidan med delade resurser ([som nås via en privat länk](#share-assets)) klickar du på en miniatyrbild för resursen och väljer ![hämta](/help/assets/assets/download-icon.svg) för att markera och visa tillgängliga dynamiska återgivningar av resursen på panelen **[!UICONTROL Download]** innan du markerar och hämtar dem.
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)


