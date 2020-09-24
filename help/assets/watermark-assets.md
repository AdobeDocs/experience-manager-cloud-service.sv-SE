---
title: Vattenstämpla dina resurser
description: Lägg till vattenstämpel i era digitala resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a9ebb97541b44140d0155bcfa5d0228c79dbffec
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Vattenstämpla dina resurser {#watermark-assets}

[!DNL Adobe Experience Manager Assets] Med kan du lägga till en digital vattenstämpel i bilder. [!DNL Assets] har stöd för att använda en bild som vattenstämpel på andra bildfiler. Vattenstämplar kan hjälpa användare att verifiera autenticitet och upphovsrättsskydd för resurserna. En vattenstämpel kan också användas för att ange ett dokuments status, t.ex. konfidentiellt, utkast, giltighet.

Så här konfigurerar du Experience Manager till vattenstämpelresurser:

1. En PNG-fil används som en vattenstämpel. Överför den här filen till DAM-databasen.

1. Gå till Cloud Manager Git-databasen som är kopplad till din miljö. Bekräfta en fil med namnet `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.json` i deras Cloud Manager Git-databas med följande innehåll. Mer information finns i [Så här gör du OSGi-konfiguration i Experience Manager som Cloud Service](/help/implementing/deploying/configuring-osgi.md).

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [Skapa en bearbetningsprofil](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) för att använda vattenstämpeln med hjälp av tillgångsmikrotjänster.

![Resursbearbetningsprofil för att skapa vattenstämpel](assets/watermark-processing-profile.png)

1. [Använd bearbetningsprofilerna på en mapp](/help/assets/asset-microservices-configure-and-use.md#use-profiles) för att skapa material med vattenstämpel.

## Tips och begränsningar {#tips-limitations-bestpractices}

* Du kan använda en enda konfiguration för att vattenstämpla alla resurser. Endast en bild används för vattenstämplar och dess bredd är fast.
* Du kan placera vattenstämpeln i mitten utan att skriva ut.
* Textbaserade vattenstämplar stöds inte.

>[!MORELIKETHIS]
>
>* [Resursmikrotjänster - översikt](/help/assets/asset-microservices-overview.md).
>* [Använd resursmikrotjänster med bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).

