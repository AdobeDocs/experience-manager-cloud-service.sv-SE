---
title: Dela resurser, mappar och samlingar som en länk
description: I den här artikeln beskrivs hur du delar resurser, mappar och samlingar i Experience Manager Assets som en hyperlänk.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Dela och distribuera resurser som hanteras i Experience Manager {#share-assets-from-aem}

Med Adobe Experience Manager Assets (AEM) kan ni dela resurser, mappar och samlingar med medlemmar i organisationen och externa enheter, inklusive partners och leverantörer. Du kan använda följande metoder för att dela resurser från Experience Manager Assets som en molntjänst:

* Dela som länk
* Hämta resurser
* Dela via AEM-datorprogrammet
* Dela via Adobe Asset Link
* (Kommande funktioner) Dela via varumärkesportalen

## Dela resurser som en länk {#sharelink}

Använd dialogrutan Länkdelning för att generera URL:en för resurser som du vill dela med användare. Användare med administratörsbehörighet eller läsbehörighet på `/var/dam/share` platsen kan visa de länkar som delas med dem. Att dela resurser via en länk är ett bekvämt sätt att göra resurser tillgängliga för externa parter utan att de först behöver logga in på AEM Assets.

>[!NOTE]
>
>* Du behöver behörigheten Redigera åtkomstkontrollista för mappen eller resursen som du vill dela som en länk.
>* Innan du delar en länk med användarna måste du kontrollera att Dag CQ Mail Service har konfigurerats. Annars inträffar ett fel.


1. I Assets-användargränssnittet väljer du den resurs som ska delas som en länk.
1. Klicka/tryck på **[!UICONTROL Dela länk]** i verktygsfältet.

   En resurslänk skapas automatiskt i fältet **[!UICONTROL Dela länk]** . Kopiera den här länken och dela den med användarna. Länkens standardförfallotid är en dag.

   Du kan också fortsätta med steg 3-7 i den här proceduren för att lägga till e-postmottagare, konfigurera förfallotiden för länken och skicka den från dialogrutan.

   >[!NOTE]
   >
   >Om en delad resurs flyttas till en annan plats slutar länken att fungera. Återskapa länken och dela den på nytt med användarna.

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

   * lokal
   * author
   * publicera
   För egenskaperna local och author anger du URL:en för den lokala instansen respektive författarinstansen. Både lokala egenskaper och författaregenskaper har samma värde om du kör en enda AEM-författarinstans. Ange publiceringsinstansens URL för publicering.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. Du kan också dela länken med flera användare.

   Om användaren är medlem i din organisation väljer du användarens e-post-ID bland de föreslagna e-post-ID:n som visas i listan under skrivområdet. För en extern användare anger du det fullständiga e-post-ID:t och väljer det sedan i listan.

   Konfigurera SMTP-serverinformationen i [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice)om du vill att e-postmeddelanden ska kunna skickas till användare.

   >[!NOTE]
   >
   >Om du anger ett e-post-ID för en användare som inte är medlem i din organisation, kommer orden&quot;Extern användare&quot; att föregås av användarens e-post-ID.

1. Ange ett ämne för den resurs du vill dela i rutan **[!UICONTROL Ämne]** .
1. Ange ett valfritt meddelande i **[!UICONTROL rutan Meddelande]** .
1. I fältet **[!UICONTROL Förfallodatum]** anger du ett förfallodatum och en förfallotid för länken med datumväljaren. Som standard är förfallodatumet inställt för en vecka från det datum du delar länken.
1. Om du vill att användarna ska kunna hämta originalbilden tillsammans med återgivningarna väljer du **[!UICONTROL Tillåt hämtning av originalfilen]**.

   >[!NOTE]
   >
   >Som standard kan användare bara hämta återgivningar av resursen som du delar som en länk.

1. Klicka på **[!UICONTROL Dela]**. Ett meddelande bekräftar att länken delas med användarna via ett e-postmeddelande.
1. Om du vill visa den delade resursen klickar/trycker du på länken i det e-postmeddelande som skickas till användaren. Den delade resursen visas på sidan **[!UICONTROL Adobe Marketing Cloud]** .

   Om du vill växla till listvyn klickar/trycker du på layoutikonen i verktygsfältet.

1. Om du vill generera en förhandsgranskning av resursen klickar/trycker du på den delade resursen. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   >[!NOTE]
   >
   >AEM stöder generering av förhandsgranskning av resurser av dessa MIME-typer: JPG, PNG, GIF, BMP, INDD, PDF och PPT. Du kan bara hämta resurser från andra MIME-typer.

1. Om du vill hämta den delade resursen klickar/trycker du på **[!UICONTROL Välj]** i verktygsfältet, klickar/trycker på resursen och sedan på **[!UICONTROL Hämta]** i verktygsfältet.
1. Om du vill visa de resurser du har delat som länkar går du till resursgränssnittet och klickar/trycker på ikonen GlobalNav. Visa navigeringsrutan genom att välja **[!UICONTROL Navigering]** i listan.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. Om du vill ta bort delningen av en resurs markerar du den och trycker/klickar på **[!UICONTROL Ta bort delning]** i verktygsfältet.

Ett meddelande bekräftar att du inte har delat resursen. Dessutom tas posten för resursen bort från listan.

## Hämta och dela resurser {#download-and-share-assets}

Användare kan hämta vissa resurser och dela dem utanför Experience Manager. Mer information finns i [Söka efter resurser](/help/assets/search-assets.md), [hur du hämtar resurser](/help/assets/download-assets-from-aem.md)och [hur du hämtar samlingar](manage-collections.md#download-a-collection)

## Dela material med kreatörer {#share-with-creatives}

Marknadsförare och andra användare kan enkelt dela godkänt material med sina kreatörer genom att

* **AEM-datorprogram**: Appen fungerar i Windows och Mac. Se Översikt över [datorprogrammet](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html). Om du vill veta hur en auktoriserad skrivbordsanvändare enkelt kan komma åt de delade resurserna läser du [Bläddra, söka och förhandsgranska resurser](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Skrivbordsanvändare kan skapa nya resurser och dela dem med sina motsvarigheter som är AEM-användare, till exempel genom att överföra nya bilder. Se [Överföra resurser med skrivbordsappen](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Adobe Asset Link**: Kreatörerna kan söka efter och använda resurser direkt inifrån Adobe InDesign, Adobe Illustrator och Adobe Photoshop.

### Bästa praxis och felsökning {#bestpractices}

* Resursmappar eller samlingar som innehåller ett tomt utrymme i namnet kanske inte delas.
* Om användarna inte kan hämta de delade resurserna bör du fråga AEM-administratören om vilka [hämtningsgränser](/help/assets/configure-asset-sharing.md#maxdatasize) som finns.
* Om du inte kan skicka e-post med länkar till delade resurser eller om de andra användarna inte kan ta emot din e-post, bör du kontakta AEM-administratören om [e-posttjänsten](/help/assets/configure-asset-sharing.md#configmailservice) är konfigurerad eller inte.
* Om du inte kan dela resurser med hjälp av länkdelningsfunktionen måste du se till att du har rätt behörighet. Se [Dela resurser](#sharelink).

<!--
Add content or link about how to share using BP, DA, AAL, etc.
-->
