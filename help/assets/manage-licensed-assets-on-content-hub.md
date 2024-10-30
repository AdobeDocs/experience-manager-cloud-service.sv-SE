---
title: Hantera licensierade Assets på Content Hub
description: Läs om olika metadatahanterings- och redigeringsmetoder
source-git-commit: 541d5819e19c67eb3f961e41000106178bff66de
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Hantera licensierade Assets på Content Hub {#manage-licensed-assets-on-content-hub}

Som administratör redigerar du metadataformuläret så att det innehåller resurslicensfältet, så att det visas i Resursegenskaper i AEM redigeringsmiljö. Du kan sedan godkänna mediefilen och dess licens för att göra den licensierad och tillgänglig på Content Hub.

Utför följande steg:

1. Redigera metadataformuläret så att det innehåller ett nytt textfält med licensinformation. Mappa textfältet till egenskapen `dc:license`. Mer information om hur du lägger till fält i ett metadataformulär och definierar egenskaper finns i [Konfigurera metadata Forms](/help/assets/metadata-assets-view.md#metadata-forms).
   ![ZIP-extrahering](/help/assets/assets/metadata-form-edit.png)
1. Använd metadataformuläret på resursmappen för att tillämpa de inställningar som ingår i steg 1. Mer information om hur du tilldelar metadataformulär till resursmappen finns i [Tilldela metadataformulär till en mapp](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Godkänn licensierade PDF](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Markera resursen och klicka på **Detaljer** för att visa dess egenskaper. I licensfältet som läggs till i steg 1 definierar du den absoluta sökvägen för den tillgångslicens som har godkänts i steg 3 eller som redan har godkänts tidigare. Content Hub absoluta sökväg följer det här standardmönstret: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Till exempel /content/dam/teamA/projects/documents/file1.pdf
   ![absolut sökväg](/help/assets/assets/absolute-path.png)


