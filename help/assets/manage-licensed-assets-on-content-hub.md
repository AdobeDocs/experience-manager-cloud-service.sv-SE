---
title: Hantera licensierade Assets på Content Hub
description: Lär dig hur du lägger till ett licensfält i metadataformuläret för mediefiler, använder metadataegenskapen Licens på objektmappar och godkänner mediefiler med licenser för användning.
badgeSaas: label="AEM Assets" type="Positive" tooltip="Gäller AEM Assets)."
exl-id: ac3aad9f-c7b3-47a7-9314-a2f8277f0d3e
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '616'
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

## Frågor och svar {#faqs-manage-licensed-assets-content-hub}

### Vad är syftet med att hantera licensierade mediefiler på AEM Assets Content Hub?

Genom att hantera licensierat material på Content Hub kan administratörer se till att endast godkänt material med giltiga licenser är tillgängligt för användning, vilket säkerställer regelefterlevnad och korrekt metadataspårning i AEM redigeringsmiljö.

### Hur lägger jag till ett licensfält i resursegenskaperna i Experience Manager as a Cloud Service?

Du kan lägga till ett licensfält i resursegenskaper genom att redigera metadataformuläret så att det innehåller ett nytt textfält som är mappat till egenskapen `dc:license`. Det här fältet visas sedan i resursegenskaperna i AEM Assets redigeringsmiljö.

### Hur använder man ett metadataformulär i en resursmapp för att inkludera licensfältet i resursegenskaperna?

Redigera metadataformuläret så att det innehåller licensfältet. Använd det här metadataformuläret på den önskade resursmappen för att se till att de nya inställningarna införlivas för alla resurser i den mappen.

### Hur anger jag licensinformation för en mediefil?

Om du vill ange licensinformation markerar du resursen, klickar på **Detaljer** för att visa dess egenskaper och anger den absoluta sökvägen för den godkända resurslicensen i licensfältet som lagts till i metadataformuläret.

### Vilket format krävs för Content Hub absoluta sökväg för en medielicens?

Content Hub absoluta sökväg ska följa mönstret: /content/dam/(Resursens mapphierarki i DAM-databasen)/(asset_name).(file_extension). Exempel: `/content/dam/teamA/projects/documents/file1.pdf`.

### Varför är det viktigt att godkänna både mediefilen och licensen för att göra dem tillgängliga på AEM Assets Content Hub?

Genom att godkänna både mediefilen och licensen säkerställs att endast korrekt licensierade och auktoriserade mediefiler finns tillgängliga på AEM Assets Content Hub, vilket bidrar till att upprätthålla regelefterlevnad och korrekta användningsrättigheter.

### Hur gör jag en mediefil tillgänglig i AEM Assets Content Hub efter att jag godkänt licensen?

När du har definierat licenssökvägen i resursens egenskaper godkänner du resursen och klickar på Spara. Den här åtgärden gör den licensierade mediefilen tillgänglig i AEM Assets Content Hub.

### Vem ansvarar för att hantera licensierade mediefiler i Content Hub?

Administratörer ansvarar för att redigera metadataformulär, tilldela dem till resursmappar och godkänna både resurser och deras licenser i Content Hub.
