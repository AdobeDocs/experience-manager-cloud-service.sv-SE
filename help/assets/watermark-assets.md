---
title: Hur vattenstämplar du dina mediefiler i AEM?
description: Lär dig hur du lägger till en digital vattenstämpel till dina resurser i AEM. Vattenstämplar kan hjälpa användare att verifiera autenticitet och upphovsrättsskydd för resurserna.
contentOwner: AG
feature: Asset Management,Publishing
role: User, Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# Vattenstämpla dina resurser {#watermark-assets}

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

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/watermarking.html) |
| AEM as a Cloud Service | Den här artikeln |

Med [!DNL Adobe Experience Manager Assets] kan du lägga till en digital vattenstämpel i bilder och videoklipp. [!DNL Assets] har stöd för att använda en bild som vattenstämpel på andra bildfiler. Vattenstämplar kan hjälpa användare att verifiera autenticitet och upphovsrättsskydd för resurserna. En vattenstämpel kan också användas för att ange ett dokuments status, t.ex. konfidentiellt, utkast, giltighet.

Så här konfigurerar du [!DNL Experience Manager] till vattenstämpelresurser:

1. En PNG-fil används som en vattenstämpel. Överför den här filen till din DAM-databas.

1. Navigera till **[!UICONTROL Tools > Assets > Assets Configurations]**.

1. Klicka på **[!UICONTROL System Watermarking Profile]**.

1. På [!UICONTROL System Watermarking Profile page] anger du bildsökvägen som ska överföras till DAM-databasen i steg 1.

1. Ange vattenstämpelskalan, från 0,0 till 1,0, i förhållande till återgivningsbredden, i fältet **[!UICONTROL Scale]**.

1. Klicka på **[!UICONTROL Save]**.

   ![Identifierare för resursduplicering](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >Om du har konfigurerat en systemvattenstämpelprofil med hjälp av konfigurationsfilen `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` (OSGi-konfiguration) kan du fortsätta att använda den, men Adobe rekommenderar att du använder den nya metoden.


1. [Skapa en bearbetningsprofil](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) om du vill använda resursmikrotjänster för att använda vattenstämpeln.

   ![Resursbearbetningsprofil för att skapa vattenstämpel](assets/watermark-processing-profile.png)

   Se till att du aktiverar växlingsknappen **[!UICONTROL Watermark]** när du skapar bearbetningsprofilen.

1. [Använd bearbetningsprofilerna på en mapp](/help/assets/asset-microservices-configure-and-use.md#use-profiles) för att skapa resurser med vattenstämpel.

## Tips och begränsningar {#tips-limitations-bestpractices}

* Du kan använda en enda konfiguration för att vattenstämpla alla resurser. Endast en bild används för vattenstämplar och dess bredd är fast.
* Du kan placera vattenstämpeln i mitten utan att skriva ut.
* Textbaserade vattenstämplar stöds inte.

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Resursmikrotjänster - översikt](/help/assets/asset-microservices-overview.md).
>* [Använd resursmikrotjänster med bearbetningsprofiler](/help/assets/asset-microservices-configure-and-use.md).
