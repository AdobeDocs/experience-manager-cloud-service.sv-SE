---
title: Vattenstämpel för resurserna
description: Lägg till vattenstämpel i era digitala resurser.
contentOwner: AG
feature: Resurshantering,publicering
role: Affärsledare,Administratör
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Vattenstämpla dina resurser {#watermark-assets}

[!DNL Adobe Experience Manager Assets] Med kan du lägga till en digital vattenstämpel i bilder. [!DNL Assets] har stöd för att använda en bild som vattenstämpel på andra bildfiler. Vattenstämplar kan hjälpa användare att verifiera autenticitet och upphovsrättsskydd för resurserna. En vattenstämpel kan också användas för att ange ett dokuments status, t.ex. konfidentiellt, utkast, giltighet.

Så här konfigurerar du [!DNL Experience Manager] till vattenstämpelresurser:

1. En PNG-fil används som en vattenstämpel. Överför den här filen till DAM-databasen.

1. Använd den [!DNL Cloud Manager] Git-databas som är kopplad till din miljö. Spara en fil med namnet `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` i databasen med följande innehåll. Instruktioner finns i [Så här gör du OSGi-konfiguration i [!DNL Experience Manager] som en [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [Skapa en ](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) bearbetningsprofil för att använda resursmikrotjänsterna för vattenstämpeln.

   ![Resursbearbetningsprofil för att skapa vattenstämpel](assets/watermark-processing-profile.png)

1. [Använd bearbetningsprofilerna på en ](/help/assets/asset-microservices-configure-and-use.md#use-profiles) mapp för att skapa material med vattenstämpel.

## Tips och begränsningar {#tips-limitations-bestpractices}

* Du kan använda en enda konfiguration för att vattenstämpla alla resurser. Endast en bild används för vattenstämplar och dess bredd är fast.
* Du kan placera vattenstämpeln i mitten utan att skriva ut.
* Textbaserade vattenstämplar stöds inte.

>[!MORELIKETHIS]
>
>* [Resursmikrotjänster - översikt](/help/assets/asset-microservices-overview.md).
>* [Använd resursmikrotjänster med bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).

