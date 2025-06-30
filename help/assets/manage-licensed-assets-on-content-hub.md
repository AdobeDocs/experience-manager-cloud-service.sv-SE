---
title: Hantera licensierade Assets på Content Hub
description: Lär dig hur du lägger till ett licensfält i metadataformuläret för mediefiler, använder metadataegenskapen Licens på objektmappar och godkänner mediefiler med licenser för användning.
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Hantera licensierade Assets på Content Hub {#manage-licensed-assets-on-content-hub}

Som administratör redigerar du metadataformuläret så att det innehåller resurslicensfältet så att det visas i Resursegenskaper i AEM författarmiljö. Du kan sedan godkänna mediefilen och dess licens för att göra den licensierad och tillgänglig på Content Hub.

Utför följande steg:

1. Redigera metadataformuläret så att det innehåller ett nytt textfält med licensinformation. Mappa textfältet till egenskapen `dc:license`. Mer information om hur du lägger till fält i ett metadataformulär och definierar egenskaper finns i [Konfigurera metadata Forms](/help/assets/metadata-assets-view.md#metadata-forms).
   ![ZIP-extrahering](/help/assets/assets/metadata-form-edit.png)
1. Använd metadataformuläret på resursmappen för att tillämpa de inställningar som ingår i steg 1. Mer information om hur du tilldelar ett metadataformulär till resursmappen finns i [Tilldela metadataformulär till en mapp](/help/assets/metadata-assets-view.md#metadata-forms).
1. [Godkänn den licensierade PDF](/help/assets/manage-organize-assets-view.md#set-asset-status)
1. Markera resursen och klicka på **Detaljer** för att visa dess egenskaper. I licensfältet som läggs till i steg 1 definierar du den absoluta sökvägen för den tillgångslicens som har godkänts i steg 3 eller som redan har godkänts tidigare. Content Hub absoluta sökväg följer det här standardmönstret: `/content/dam/(The asset's folder hierarchy within the DAM repository)/(asset_name).(file_extension)`. Till exempel /content/dam/teamA/projects/documents/file1.pdf
   ![absolut sökväg](/help/assets/assets/absolute-path.png)
1. Godkänn resursen så att den blir tillgänglig i Content Hub och klicka på **Spara**. Mer information om hur du godkänner en resurs finns i [Ange resursstatus](/help/assets/manage-organize-assets-view.md#set-asset-status).
