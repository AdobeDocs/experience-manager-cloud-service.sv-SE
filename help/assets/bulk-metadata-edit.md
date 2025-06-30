---
title: Redigera flera metadata i  [!DNL Assets View]
description: Lär dig hur du kan uppdatera en fördefinierad uppsättning standardmetadatafält för flera resurser som finns på [DNL! Assets View] samtidigt.
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Redigera flera metadata i [!DNL Assets View]{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

Funktionen **[!DNL Bulk Metadata Edit]** i [!DNL Assets View] gör att du kan redigera en fördefinierad uppsättning med standardmetadatafält för flera resursfiler samtidigt. Välj flera resurser och uppdatera deras fördefinierade standarduppsättning med standardmetadata samtidigt i stället för att uppdatera standardmetadata för varje resurs separat. Denna funktion bibehåller effektiviteten, enhetligheten och exaktheten hos standardegenskaperna för metadata i de stora materialuppsättningarna, vilket förbättrar sökbarheten och organisationen för dessa resurser.

## Redigera metadata för resurser gruppvis {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

Utför de här stegen för att massredigera metadata för flera resurser samtidigt:

1. Navigera till **[!DNL Assets View]** och klicka på **[!UICONTROL Assets]**.
1. Bläddra efter specifika resurser eller sök efter dem med hjälp av nyckelord i sökfältet.
1. Markera resurserna och klicka på **[!UICONTROL Bulk Metadata Edit]** på den övre menyn.
   ![bulk-metadata-edit](/help/assets/assets/bulk-metadata-edit1.png)
1. Redigera följande fält på panelen [!UICONTROL Edit metadata page]:**[!UICONTROL Properties]**
   * **[!UICONTROL Status]:** Välj en status för de valda resurserna.
   * **[!UICONTROL Expiration date]:** Ange ett datum efter vilket resurserna inte längre är giltiga eller nödvändiga.
   * **[!UICONTROL Author]:** Ange författarens namn.
   * **[!UICONTROL Keywords]:** Lägg till specifika termer eller textsträngar som ger högnivåinformation om resurserna för att förbättra deras upptäckbarhet. Lägg till ett nyckelord och tryck på **Retur** eller **return** för att lägga till ytterligare ett nyckelord i listan.
   * **[!UICONTROL Tags]:** Klicka på ![redigera massmetadata](/help/assets/assets/tags-icon.svg) för att välja taggar bland de tillgängliga alternativen. Taggar ger mer specifik information om resurserna och gör det lättare att hitta dem. Taggar som redan används för de markerade resurserna visas på panelen **[!UICONTROL Properties]**. Om du inte hittar de relevanta taggarna skapar du dem och tilldelar till de valda resurserna. Mer information om hur du skapar och tilldelar taggar till resurser finns i [Hantera taggar i [!DNL Assets view]](/help/assets/tagging-management-assets-view.md).
   * Klicka på **[!UICONTROL Save]** om du vill använda metadatauppdateringarna ovan på de markerade resurserna. När informationen har sparats läggs **[!UICONTROL Keywords]** och **[!UICONTROL Tags]** till medan den uppdaterade informationen för **[!UICONTROL Status]**, **[!UICONTROL Expiration date]** och **[!UICONTROL Author]** åsidosätter den befintliga informationen.
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >Du kan redigera metadata för 100 resurser i taget.

Om du vill visa de metadatauppdateringar som används för en resurs går du till [!DNL asset details page] (markera resursen och klickar på **[!UICONTROL Details]**) och klickar på ![redigera massmetadata](/help/assets/assets/info-icon-solid-black.svg) för att visa resursens metadata på panelen **[!UICONTROL Information]**.

>[!NOTE]
>
>**[!UICONTROL Status]**, **[!UICONTROL Expiration date]**, **[!UICONTROL Author]**, **[!UICONTROL Keywords]** och **[!UICONTROL Tags]** är standardmetadataegenskaper som är tillgängliga för redigering av massmetadata, oavsett mappspecifika metadata. Dessa metadataegenskaper visas bara på [!UICONTROL asset details page] om de ingår i metadataformuläret som används i resursens mapp. Om du inte kan hitta dessa standardmetadataegenskaper på [!UICONTROL asset details page] redigerar du resursmappens metadataformulär så att de inkluderas. Mer information om hur du skapar eller redigerar ett metadataformulär och använder det på en mapp finns i [Metadata i [!DNL Assets View]](/help/assets/metadata-assets-view.md).
