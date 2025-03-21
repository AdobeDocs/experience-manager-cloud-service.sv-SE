---
title: Redigera flera metadata i Assets View
description: Lär dig hur du kan uppdatera en fördefinierad uppsättning med standardmetadatafält för flera resurser som är tillgängliga i Assets View samtidigt.
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# Redigera flera metadata i Assets View{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime och Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets-integrering med Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI-utökningsbarhet</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nytt</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Aktivera Dynamic Media Prime och Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Sök efter bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Metadata - bästa praxis</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamiska media med OpenAPI-funktioner</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets-dokumentation för utvecklare</b></a>
        </td>
    </tr>
</table>

Med funktionen **Redigera massmetadata** i Assets-vyn kan användare redigera en fördefinierad uppsättning standardmetadatafält för flera resursfiler samtidigt. Välj flera resurser och uppdatera deras fördefinierade standarduppsättning med standardmetadata samtidigt i stället för att uppdatera standardmetadata för varje resurs separat. Den här funktionen förbättrar effektiviteten, enhetligheten och exaktheten i standardmetadataegenskaperna i en stor uppsättning resurser, vilket förbättrar sökbarheten och organisationen av resurser.

## Redigera metadata för resurser gruppvis {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

Utför de här stegen för att massredigera metadata för flera resurser samtidigt:

1. Klicka på **Assets** i Assets-vyn.
1. Bläddra efter specifika resurser eller sök efter dem med hjälp av nyckelord i sökfältet.
1. Markera resurserna och klicka på **Redigera massmetadata** på den översta menyn.
   ![bulk-metadata-edit](/help/assets/assets/bulk-metadata-edit1.png)
1. Redigera följande fält på panelen **Egenskaper** på sidan Redigera metadata:
   * **Status:** Välj en status för de valda resurserna.
   * **Förfallodatum:** Ange ett datum efter vilket resurserna inte längre är giltiga eller nödvändiga.
   * **Författare:** Ange författarens namn.
   * **Nyckelord:** Lägg till specifika termer eller textsträngar som ger högnivåinformation om resurserna för att förbättra deras upptäckbarhet. Lägg till ett nyckelord och tryck på Enter eller Retur för att lägga till ett annat nyckelord i listan.
   * **Taggar:** Klicka på ![taggikonen](/help/assets/assets/tags-icon.svg) för att välja taggar bland de tillgängliga alternativen. Taggar ger mer specifik information om resurserna och gör det lättare att hitta dem. Taggar som redan används för de markerade resurserna visas på panelen **Egenskaper**. Om du inte kan hitta de relevanta taggarna skapar du dem och tilldelar till de valda resurserna. Mer information om hur du skapar och tilldelar taggar till resurser finns i [Hantera taggar i vyn Assets](/help/assets/tagging-management-assets-view.md).
   * Klicka på **Spara** för att använda metadatauppdateringarna ovan på de markerade resurserna. När nyckelord och taggar har sparats läggs de till medan den uppdaterade informationen för Status, Förfallodatum och Författare åsidosätter den befintliga informationen.
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >Du kan redigera metadata för 100 resurser i taget.

Om du vill visa de metadatauppdateringar som används för en resurs går du till sidan med resursinformation (markera resursen och klickar på **Detaljer**) och klickar på ![](/help/assets/assets/info-icon-solid-black.svg) för att visa resursens metadata på panelen **Information** .

>[!NOTE]
>
>**Status**, **Förfallodatum**, **Författare**, **Nyckelord** och **Taggar** är standardmetadataegenskaper som är tillgängliga för redigering av massmetadata, oavsett mappspecifika metadata. Dessa metadataegenskaper visas bara på sidan med resursinformation om de ingår i metadataformuläret som används i resursens mapp. Om du inte kan hitta dessa standardmetadataegenskaper på sidan med resursinformation redigerar du objektmappens metadataformulär så att de inkluderas. Mer information om hur du skapar eller redigerar ett metadataformulär och använder det på en mapp finns i [Metadata i Assets View](/help/assets/metadata-assets-view.md) .
