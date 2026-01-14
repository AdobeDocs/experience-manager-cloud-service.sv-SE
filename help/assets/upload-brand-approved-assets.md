---
title: Överför varumärkesgodkända resurser till  [!DNL Content Hub]
description: Lär dig hur du överför varumärkesgodkända mediefiler till Content Hub
role: User
exl-id: f1be7cfc-1803-4c17-bb58-947104aa883c
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Överför varumärkesgodkända mediefiler till Content Hub {#upload-brand-approved-assets-content-hub}

>[!CONTEXTUALHELP]
>id="upload_assets_content_hub"
>title="Överför varumärkesgodkända mediefiler till Content Hub"
>abstract="Lägg till godkända mediefiler i Content Hub antingen från det lokala filsystemet eller importera mediefiler från OneDrive eller Dropbox datakällor. Alla resurser visas på den översta nivån i Content Hub, oavsett mappstrukturen, för att förbättra sökfunktionerna."

[Content Hub-användare med behörighet att lägga till resurser](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) kan lägga till resurser i Content Hub antingen från det lokala filsystemet eller importera resurser från OneDrive eller Dropbox-datakällor. Alla resurser visas på den översta nivån i Content Hub, oavsett vilken mappstruktur som finns i det lokala filsystemet eller datakällorna i OneDrive och Dropbox, vilket förbättrar sökfunktionerna.

Resurserna som markerats som `Approved` i Assets as a Cloud Service är automatiskt tillgängliga i Content Hub. Mer information finns i [Godkänn resurser för Content Hub](/help/assets/approve-assets-content-hub.md).

Om du vill förbättra resurssökningen ytterligare kan du göra följande med Content Hub:

* Definiera nyckeldetaljer som är relevanta för resursuppladdningen, till exempel kampanjnamn, nyckelord, kanaler och så vidare.

* Generera automatiskt fler egenskaper för varje resurs när den har överförts, till exempel filstorlek, format, upplösning och andra egenskaper.

* Använd artificiell intelligens från [Adobe AI](https://business.adobe.com/ai/adobe-genai.html) för att automatiskt tillämpa relevanta taggar på alla dina överförda resurser. Dessa taggar, som kallas smarta taggar, ökar innehållshastigheten i dina projekt genom att hjälpa dig att snabbt hitta relevanta resurser.

Se till att du bara överför dina [varumärkesgodkända resurser till Content Hub](/help/assets/approve-assets.md).

![Överför varumärkesgodkända resurser](assets/upload-brand-approved-assets.png)

## Förutsättningar {#prerequisites-add-assets}

[Content Hub-användare med behörighet att lägga till resurser](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) kan överföra resurser till Content Hub.

## Lägga till resurser i Content Hub från det lokala filsystemet {#add-assets-local-file-system}

Så här lägger du till resurser i Content Hub:

1. Klicka på **[!UICONTROL Add Assets]** om du vill visa dialogrutan **[!UICONTROL Add your approved assets]** där du kan skapa en överföring.

1. I avsnittet **[!UICONTROL Drag files or folders here]** som är tillgängligt i den högra rutan kan du antingen dra resurserna från det lokala filsystemet eller klicka på **[!UICONTROL Browse]** för att manuellt välja filer eller mappar som är tillgängliga i det lokala filsystemet. Den här listan över filer som ingår i överföringen finns som en lista.


   Du kan också förhandsvisa markerade bilder med hjälp av miniatyrbilderna och klicka på X-ikonen för att ta bort en viss bild från listan. X-ikonen visas bara när du håller muspekaren över bildens namn eller storlek. Du kan också klicka på **[!UICONTROL Remove all]** om du vill ta bort alla objekt från överföringslistan.

   Om du vill slutföra överföringsprocessen och aktivera **[!UICONTROL Upload button]** måste du gruppera dina resurser under ett kampanjnamn.

   ![Överför resurser till Content Hub](assets/upload-assets-content-hub.png)

1. Definiera namnet på din överföring med fältet **[!UICONTROL Campaign name]**. Du kan använda ett befintligt namn eller skapa ett nytt. I Content Hub finns fler alternativ när du skriver namnet. <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   Adobe rekommenderar att du anger värden i resten av fälten och skapar en förbättrad sökupplevelse för dina överförda resurser.

1. Definiera värden för fälten **[!UICONTROL Keywords]**, **[!UICONTROL Channels]**, **[!UICONTROL Timeframe]** och **[!UICONTROL Region]**. Genom att tagga och gruppera resurser efter nyckelord, kanaler och plats kan alla som använder ditt godkända företagsinnehåll hitta och ordna mediefilerna.

1. Klicka på **[!UICONTROL Upload]** om du vill överföra resurser till Content Hub. [!UICONTROL Review details] bekräftelseruta visas. Klicka på [!UICONTROL Continue].

1. Assets börjar ladda upp. Klicka på [!UICONTROL New Upload] för att starta om överföringsproceduren. Klicka på [!UICONTROL Done] för att slutföra överföringen.

Administratörer kan också konfigurera obligatoriska och valfria fält som visas när resurser överförs, som kampanjnamn, nyckelord, kanaler och så vidare. Mer information finns i [Konfigurera Content Hub användargränssnitt](configure-content-hub-ui-options.md#configure-upload-options-content-hub).

## Hantera resurser som överförts med Content Hub {#manage-assets-uploaded-using-content-hub}

[Content Hub-användare med behörighet att lägga till resurser](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) kan [lägga till resurser i Content Hub](/help/assets/upload-brand-approved-assets.md) antingen från det lokala filsystemet eller importera resurser från OneDrive eller Dropbox-datakällor. Alla resurser visas på den översta nivån i Content Hub, oavsett vilken mappstruktur som finns i det lokala filsystemet eller datakällorna i OneDrive och Dropbox, vilket förbättrar sökfunktionerna.

Visningen av resurser som överförts med Content Hub beror på om du har [aktiverat alternativet för automatiskt godkännande](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub):

* Om växlingsknappen **[!UICONTROL Auto-approval]** är aktiverad blir de resurser som du överför med Content Hub automatiskt tillgängliga.

* Om **[!UICONTROL Auto-approval]**-växeln är inaktiverad visas inte de resurser som du överför med Content Hub automatiskt. Resurserna är tillgängliga i mappen `hydrated-assets` i din Assets as a Cloud Service-miljö. Navigera till mappen och [massredigera](#bulk-approve-assets-content-hub) statusen för dessa resurser till `Approved` för de resurser som ska visas i Content Hub.

![Content Hub godkännandeprocess](/help/assets/assets/content-hub-approval.png)
