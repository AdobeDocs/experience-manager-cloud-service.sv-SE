---
title: Överför varumärkesgodkända resurser till [!DNL Content Hub]
description: Lär dig hur du överför varumärkesgodkända mediefiler till Content Hub
role: User
source-git-commit: c85b4e1c828ed1fb7f4063f965fe116215ca0244
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---


# Överför varumärkesgodkända mediefiler till Content Hub {#upload-brand-approved-assets-content-hub}

[Content Hub-användare med rättigheter att lägga till resurser](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) kan lägga till resurser i Content Hub antingen från det lokala filsystemet eller importera resurser från datakällor i OneDrive eller Dropbox. Alla resurser visas på den översta nivån i Content Hub, oavsett vilken mappstruktur som finns i det lokala filsystemet eller datakällorna OneDrive och Dropbox för att förbättra sökfunktionerna.

Om du vill förbättra resurssökningen ytterligare kan du göra följande med Content Hub:

* Definiera nyckeldetaljer som är relevanta för resursuppladdningen, till exempel kampanjnamn, nyckelord, kanaler och så vidare.

* Generera automatiskt fler egenskaper för varje resurs när den har överförts, till exempel filstorlek, format, upplösning och andra egenskaper.

* Använd artificiell intelligens från [Adobe Sensei](https://www.adobe.com/sensei.html) för att automatiskt lägga till relevanta taggar i alla dina överförda resurser. Dessa taggar, som kallas smarta taggar, ökar innehållshastigheten i dina projekt genom att hjälpa dig att snabbt hitta relevanta resurser.

Se till att du bara överför dina [varumärkesgodkänt material till Content Hub](/help/assets/approve-assets.md).

![Överför varumärkesgodkända resurser](assets/upload-brand-approved-assets.png)

## Förutsättningar {#prerequisites-add-assets}

[Content Hub-användare med rättigheter att lägga till resurser](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) kan överföra resurser till Content Hub.

## Lägga till resurser i Content Hub från det lokala filsystemet {#add-assets-local-file-system}

Så här lägger du till resurser i Content Hub:

1. Klicka **[!UICONTROL Add Assets]** för att visa **[!UICONTROL Add your approved assets]** som gör att du kan skapa en överföring.

1. I **[!UICONTROL Drag files or folders here]** i det högra fönstret kan du antingen dra resurserna från det lokala filsystemet eller klicka på **[!UICONTROL Browse]** om du manuellt vill välja filer eller mappar som är tillgängliga i det lokala filsystemet. Den här listan över filer som ingår i överföringen finns som en lista.


   Du kan också förhandsvisa markerade bilder med hjälp av miniatyrbilderna och klicka på X-ikonen för att ta bort en viss bild från listan. X-ikonen visas bara när du håller muspekaren över bildens namn eller storlek. Du kan också klicka **[!UICONTROL Remove all]** om du vill ta bort alla objekt från överföringslistan.

   För att slutföra överföringen och aktivera **[!UICONTROL Upload button]** måste du gruppera dina resurser under ett Campaign-namn.

   ![Överför resurser till Content Hub](assets/upload-assets-content-hub.png)

1. Definiera namnet på överföringen med **[!UICONTROL Campaign name]** fält. Du kan använda ett befintligt namn eller skapa ett nytt. I Content Hub finns fler alternativ när du skriver namnet. <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   Som en god praxis rekommenderar Adobe att du anger värden i resten av fälten, liksom att du får en förbättrad sökupplevelse för dina överförda resurser.

1. Definiera på liknande sätt värden för **[!UICONTROL Keywords]**, **[!UICONTROL Channels]**, **[!UICONTROL Timeframe]** och **[!UICONTROL Region]** fält. Genom att tagga och gruppera resurser efter nyckelord, kanaler och plats kan alla som använder ditt godkända företagsinnehåll hitta och ordna mediefilerna.

1. Klicka **[!UICONTROL Upload]** för att ladda upp material till Content Hub. [!UICONTROL Review details] bekräftelserutan visas. Klicka på [!UICONTROL Continue].

1. Assets börjar ladda upp. Klicka [!UICONTROL New Upload] för att starta om överföringsproceduren. Klicka [!UICONTROL Done] för att slutföra överföringen.

Administratörer kan också konfigurera obligatoriska och valfria fält som visas när resurser överförs, som kampanjnamn, nyckelord, kanaler och så vidare. Mer information finns i [Konfigurera Content Hub användargränssnitt](configure-content-hub-ui-options.md#configure-upload-options-content-hub).


## Lägga till resurser i Content Hub från datakällor i OneDrive eller Dropbox {#add-assets-onedrive-dropbox}

Så här lägger du till resurser i Content Hub från datakällor i OneDrive eller Dropbox:

1. Klicka **[!UICONTROL Add Assets]** för att visa **[!UICONTROL Add your approved assets]** som gör att du kan importera resurser från OneDrive eller Dropbox.

1. Klicka **[!UICONTROL OneDrive]** eller **[!UICONTROL Dropbox]** för att starta importprocessen. Content Hub uppmanar dig att logga in på ditt OneDrive- eller Dropbox-konto och visar sedan mappstrukturen OneDrive eller Dropbox i den vänstra rutan.

1. Klicka på ikonen + bredvid filen eller mappnamnet för att visa objektet i listan med valda objekt. När du har valt alla filer som du behöver lägga till i Content Hub-portalen upprepar du steg 3 till 6 i [Lägga till resurser i Content Hub från det lokala filsystemet](#add-assets-local-file-system) för att slutföra överföringsprocessen.

   ![Överför resurser till Content Hub från OneDrive eller Dropbox](assets/add-assets-onedrive-dropbox.png)

Administratörer kan också konfigurera obligatoriska och valfria fält som visas när resurser överförs, som kampanjnamn, nyckelord, kanaler och så vidare. Mer information finns i [Konfigurera Content Hub användargränssnitt](configure-content-hub-ui-options.md#configure-upload-options-content-hub).

