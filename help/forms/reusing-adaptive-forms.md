---
title: Återanvända metadataegenskaper i ett adaptivt formulär
seo-title: Reuse metadata properties of an Adaptive Form
description: Du kan återanvända ett befintligt adaptivt formulär för att skapa ett nytt adaptivt Forms.
seo-description: You can reuse an existing Adaptive Form to create new Adaptive Forms.
exl-id: fb8cf3a9-fd19-46bf-b40e-2af76ca68b9f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Återanvända metadataegenskaper i ett adaptivt formulär {#reusing-adaptive-forms}

Om du vill använda vissa av egenskaperna i ett befintligt adaptivt formulär för att skapa ett nytt, behöver du bara använda funktionen för att kopiera och klistra in. Dessutom kan du klistra in det nya adaptiva formuläret i önskad mappsökväg. Alla metadataegenskaper replikeras och XFA- och XSD-värdena för XFA- och XSD-baserade adaptiva Forms kopieras också.

>[!NOTE]
>
>Status och granskningsinformation kopieras inte. Om det adaptiva formuläret till exempel publiceras och sedan kopieras, är det inklistrade adaptiva formuläret inte publicerat. På samma sätt gäller att om en kopierad resurs håller på att granskas är den inklistrade resursen inte under samma granskning.

## Kopiera ett anpassat formulär {#copy-an-adaptive-form}

Kopiera ett adaptivt formulär på något av följande sätt:

1. Klicka på Kopiera ![aem6forms_copy](assets/aem6forms_copy.png) -ikon från snabbåtgärder.

   >[!NOTE]
   >
   >Snabbåtgärder är de åtgärdsobjekt som visas över en miniatyrbild när du håller muspekaren.

1. Välj det adaptiva formuläret. Markeringsprocessen är annorlunda för olika vyer.

   Om du arbetar i kortvyn går du till markeringsläget genom att klicka på markeringen ![aem6forms_check-circle](assets/aem6forms_check-circle.png) och klicka på alla adaptiva Forms som du vill kopiera.

   Om du är i listvyn markerar du kryssrutorna för alla adaptiva Forms.

   >[!NOTE]
   >
   >Alla markerade resurser måste vara Adaptiv Forms eftersom funktionen kopiera och klistra in bara stöds för Adaptiv Forms, och alla markerade resurser måste finnas i samma mapp.

   När du har valt resurserna klickar du på kopian ![aem6forms_copy](assets/aem6forms_copy.png) ikonen finns i verktygsfältet för att kopiera det markerade adaptiva formuläret.

## Klistra in ett anpassat formulär {#paste-an-adaptive-form}

När du klickar på kopieringsåtgärden avslutas markeringsläget automatiskt och klistra in ![Klistra in](assets/Smock_Paste_18_N.svg) -ikonen visas. Gå till önskad mappsökväg och klicka på Klistra in ![Klistra in](assets/Smock_Paste_18_N.svg) om du vill klistra in det kopierade adaptiva formuläret.

Om du klistrar in i samma mapp eller en annan fil med samma nodnamn (som den lagras i CRX-databasen med) finns i den här målmappen läggs 1 till i suffixet (till exempel blir myaf1 och om myaf1 finns på samma plats blir myaf2. Alla andra egenskaper är desamma som den ursprungliga adaptiva formen.

När du klickat på Klistra in ![Klistra in](assets/Smock_Paste_18_N.svg) kommer den att döljas igen. Du kan bara klistra in en gång. Om du vill skapa en kopia av samma resurs kopierar du den igen.

## Ändra innehållet i det nya adaptiva formuläret {#change-contents-of-new-adaptive-form}

Innehållet i en inklistrad adaptiv Forms kan ändras på följande sätt så att det skiljer sig från det kopierade formuläret:

1. **Ändra metadataegenskaper:**

   Du kan ändra metadataegenskaperna för det adaptiva formuläret, till exempel rubrik och beskrivning. Mer information om metadataegenskaper och hur de kan ändras finns i [Hantera formulärmetadata](manage-form-metadata.md)

1. **Ändra XFA/XSD för XFA/XSD-baserad Adaptive Forms:**

   Du kan ändra den XFA/XSD som används i Adaptiv Forms. Om du vill veta hur dessa adaptiva Forms kan ändras går du till [Hantera formulärmetadata](manage-form-metadata.md)

1. **Publicera igen:**

   Den inklistrade resursen skiljer sig från den kopierade. Du kan publicera den som en ny resurs för att göra den tillgänglig för slutanvändare. Så här publicerar du en resurs: <!-- see [Publishing and unpublishing forms](publishing-unpublishing-forms.md) -->
