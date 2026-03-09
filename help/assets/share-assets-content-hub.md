---
title: Dela Assets i [!DNL the Content Hub]
description: Dela Assets i [!DNL the Content Hub]
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="Gäller AEM Assets)."
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Dela resurser i Content Hub {#search-assets-as-a-link}

Skapa en länk till valda resurser för att enkelt dela dem med andra. Som auktoriserad [!DNL Content Hub]-användare väljer du en eller flera resurser som är tillgängliga i din [!DNL Content Hub]-miljö, skapar en länk och skickar den till andra privata eller offentliga användare.

>[!VIDEO](https://video.tv.adobe.com/v/3474890/?learn=on&enablevpops=on){transcript=true}

## Förutsättningar {#prerequisites}

[Content Hub-användare](deploy-content-hub.md#onboard-content-hub-users) kan skapa en länk till markerade resurser och dela den med andra användare.

## Dela resurser {#share-assets}

Så här delar du en eller flera resurser med privata eller offentliga användare:

1. Navigera till din [!DNL Content Hub]-hemsida, markera en eller flera resurser och klicka på ![ dela ](/help/assets/assets/share.svg) **[!UICONTROL Share]** för att visa en enskild markerad resurs eller en lista med flera markerade resurser i dialogrutan **[!UICONTROL Share assets]** .

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

## Frågor och svar {#faqs-share-assets-content-hub}

### Vad innebär delning av resurser i AEM Assets Content Hub?

Genom att dela resurser i AEM Assets Content Hub kan behöriga användare enkelt dela en eller flera resurser eller hela samlingar med andra genom att skapa en länk. Den här länken kan skickas till privata användare (som måste logga in) eller offentliga användare (som kan komma åt som gäster), vilket ger mottagarna direktåtkomst för att visa och hämta de valda resurserna.

### Hur delar jag resurser och samlingar med andra via AEM Assets Content Hub?

Om du vill dela resurser eller samlingar i Content Hub går du till Content Hub hemsida, markerar en eller flera resurser (eller går till fliken Samlingar för samlingar) och klickar på ikonen Dela. I dialogrutan Dela kan du förhandsgranska resurserna, ta bort eventuella resurser, lägga till en titel och en beskrivning, välja vem som kan komma åt länken (privat eller offentlig), ange en förfalloperiod och sedan klicka på Hämta länk för att generera och kopiera den delningsbara URL:en. Länken kan sedan skickas till teammedlemmar eller intressenter.

### Vilka åtkomstalternativ är tillgängliga när du delar resurser i AEM Assets Content Hub och hur skiljer de sig åt?

I Content Hub kan du välja mellan två åtkomstalternativ för delade länkar: privata och offentliga. Privata länkar kräver att mottagarna loggar in i sin Content Hub-miljö för att visa och hämta resurser, vilket ger ökad säkerhet. Alla som har länken kan komma åt offentliga länkar utan att det krävs inloggning. Varje länktyp har sina egna förfalloinställningar, till exempel 24 timmar till en vecka för offentliga länkar och anpassade datum för privata länkar.

### Hanteras någon konfiguration av administratören för att kunna generera offentliga länkar för resurser i AEM Assets Content Hub?

Ja, administratörer kan aktivera eller inaktivera alternativet **Aktivera offentlig länk** som finns på fliken **Samlingar och delning** i konfigurationsgränssnittet för att hantera genereringen av offentliga länkar för resurser i AEM Assets Content Hub.

### Kan jag ange förfallodatum för delade resurslänkar i AEM Assets Content Hub och varför är detta viktigt?

Ja, du kan ange förfallodatum för både privata och offentliga delade länkar i Content Hub. För offentliga länkar kan du välja bland förinställningar som 24 timmar upp till en vecka, medan du med hjälp av privata länkar kan välja bland förinställningar eller ange ett anpassat förfallodatum. Förfallodatum är viktiga eftersom länken inte längre kan användas för att komma åt eller hämta resurserna när den upphör att gälla, vilket bidrar till att upprätthålla säkerheten och kontrollen för ditt innehåll.

### Vad kan mottagarna göra med den delade resurslänken som skapats med AEM Assets Content Hub, och finns det alternativ för att hämta olika återgivningar?

Mottagare som tar emot en delad resurslänk kan öppna den i sin webbläsare och förhandsgranska, välja och hämta de resurser som finns. Om resursåtergivningar är aktiverade i Content Hub kan mottagarna välja vilka återgivningar (till exempel Original eller Static) de vill hämta. Resurserna och återgivningarna hämtas som en zip-fil och metadata kan visas genom att du klickar på miniatyrbilden för resursen. Länken fungerar tills det angivna förfallodatumet.




