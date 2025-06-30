---
title: Importera metadataformulär från [!DNL Admin View] till [!DNL Assets View]
description: I den här artikeln beskrivs hur du importerar metadataformuläret från [!DNL Admin View] till [!DNL Assets View]
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 5fb4fe97-486a-4a91-af60-a7182efcc2f9
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Importera metadata från [!DNL Admin View] till [!DNL Assets View] {#import-metadata-forms-from-admin-view-to-assets-view}

Med [!DNL Adobe Experience Manager Assets] kan du importera metadataformulär och deras mappassociationer från [!DNL Admin View] till [!DNL Assets View].

## Innan du börjar{#prerequisites-for-importing-metadata-forms-to-assets-view}

Kontrollera att du har administratörsbehörighet för att importera metadataformulär och mappassociationer för dem från [!DNL Admin View] till [!DNL Assets View].

## Importera metadataformulär till [!DNL Assets View]{#import-metadata-forms-to-assets-view}

Som administratör ska du utföra följande steg för att importera metadataformulär som är tillgängliga i [!DNL Admin View] till [!DNL Assets View]:

1. Navigera till startsidan för [!DNL Assets View] och klicka på **[!UICONTROL &#x200B; Metadata Forms]** under **[!UICONTROL Settings]** för att öppna sidan **[!UICONTROL Metadata Forms]** med en lista över metadataformulär som är tillgängliga i [!DNL Assets View].

   ![sida med metadataformulär](/help/assets/assets/metadata-forms-page.png)

1. Välj **[!UICONTROL Import]**, ett bearbetningsmeddelande visas (till exempel *Bearbetar 2 metadataformulär ... Vänta.*) medan importen pågår. När bearbetningen är klar visas tabellen **[!UICONTROL Import metadata forms]**, som innehåller en lista med metadataformulär som är tillgängliga i [!DNL Admin View]. Tabellraden innehåller namn på metadataformulär (under **[!UICONTROL Name]**), mappar som är kopplade till det formuläret (under **[!UICONTROL Folder Association]**) och ett alternativ för att förhandsgranska ![förhandsgranska](/help/assets/assets/Preview.svg) formuläret innan det importeras.

   ![Importera Forms-metadatasida](/help/assets/assets/import-metadata-forms-page.png)

   >[!NOTE]
   > 
   > I **[!UICONTROL Import Metadata Forms]**-tabellen visas en **[!UICONTROL Duplicate]**-etikett bredvid ett formulärnamn att formuläret redan används i en mapp i [!DNL Assets View]. Om du importerar det duplicerade formuläret åsidosätts det befintliga som används i mappen. Du kan undvika den här åsidosättningen genom att ändra formulärets namn innan du importerar det. Klicka på formulärnamnet för att byta namn på det.

1. Klicka på ![välj mapp](/help/assets/assets/x.svg) bredvid ett mappnamn (under [!UICONTROL Folder Association]) för att ta bort mappkopplingen till formuläret.
1. Klicka på ![välj mapp](/help/assets/assets/add-to-folder.svg) för att välja en mapp som ska tilldelas motsvarande metadataformulär.
1. Klicka på den röda cirkeln om du vill visa information om metadatakomponenter eller mappningar i formuläret som inte stöds och som har undantagits från importen.

   ![Importera Forms-metadatasida](/help/assets/assets/unsupported-import-elements.png)

1. Markera ett eller flera formulär i tabellen och klicka på **[!UICONTROL Start Import]** för att importera metadataformulären och tillhörande mappar till [!DNL Assets View]. Ett bearbetningsmeddelande visas (till exempel *Importera 3 metadataformulär. Vänta!*). När importen är klar bekräftar ett meddelande att formulären har importerats och sidan **[!UICONTROL Metadata Forms]** (av [!DNL Assets View]) visar både nyligen importerade och befintliga formulär som är tillgängliga i [!DNL Assets View]. Du kan göra följande på den här sidan:

   * Klicka på kolumnrubriken om du vill sortera tabellen efter [!UICONTROL Name], [!UICONTROL Modified] eller [!UICONTROL Author].
   * Markera det importerade formuläret, klicka på **[!UICONTROL Remove from folder(s)]** och kontrollera sedan mappnamnet i mappsökvägen för att bekräfta att mappen är korrekt porterad.

     ![verifiera sidan med metadataformulär](/help/assets/assets/confirm-ported-folder.png)
   * Markera det importerade formuläret och klicka på **[!UICONTROL Edit]** för att visa alla konfigurationer som stöds av metadataformuläret. Mer information om metadataformulär, deras komponenter och fält finns i [Konfigurera metadata-Forms](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/metadata#metadata-forms).

   ![verifiera sidan med metadataformulär](/help/assets/assets/verify-metadata-forms-page.png)

## Verifiera importerade metadataformulär{#Verify-the-imported-metadata-forms}

När du har importerat metadataformulär från [!DNL Admin View] till [!DNL Assets View] följer du de här stegen för att verifiera importen:

1. Navigera till någon av de associerade mapparna i det importerade metadataformuläret.
1. Navigera till informationssidan för en [resurs](/help/assets/navigate-assets-view.md#preview-assets) och verifiera att de metadatakomponenter, komponentfält och fältvärden som stöds synkroniseras från [!DNL Admin View]. Mer information om metadatakomponenter, komponentfält och fältvärden finns i artikeln [Metadata i Resurser Essentials](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/metadata) .

   >[!NOTE]
   >
   > I [[!DNL Assets View] informationssidan](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/metadata-assets-view#metadata-forms) eller egenskapssidan [[!DNL Admin View] ](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/administer/metadata-schemas) synkroniseras ändringar av egenskapsvärden för metadata automatiskt mellan de två gränssnitten. Strukturella ändringar i formuläret, som att lägga till eller ta bort fält eller andra ändringar, synkroniseras inte.
