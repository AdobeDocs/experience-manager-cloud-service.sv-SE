---
title: Konfigurera Dynamic Media
description: Om du vill konfigurera Dynamic Media måste du konfigurera Dynamic Media och hantera bild- och visningsförinställningar.
contentOwner: Rick Brough
feature: Configuration,Viewer Presets,Image Presets,Dynamic Media
role: Admin,User
exl-id: 83b70b17-7ee3-41cb-be90-c92ca161660e
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Konfigurera Dynamic Media {#setting-up-dynamic-media}

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

{{work-with-dynamic-media}}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) hjälper dig att hantera resurser genom att leverera visuella marknadsförings- och marknadsföringsresurser på begäran, automatiskt skalade för konsumtion på webben, mobiler och sociala webbplatser. Med hjälp av en uppsättning primära källresurser genererar och levererar Dynamic Media flera varianter av multimediematerial i realtid via sitt globala, skalbara, prestandaoptimerade nätverk.

<!-- OBSOLETE UNTIL THE INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE

>[!NOTE]
>
>This documentation describes Dynamic Media capabilites, which are integrated directly into [!DNL Experience Manager]. If you are using Dynamic Media Classic (previously called Scene7) integrated into [!DNL Experience Manager], see [Dynamic Media Classic integration documentation](/help/sites-cloud/administering/integrating-scene7.md).
>
>See [Dual Use Scenario](/help/sites-cloud/administering/integrating-scene7.md#dual-use-scenario) for times when you may want to use [!DNL Experience Manager] integrated with Dynamic Media Classic along with Dynamic Media.

-->

Om du administrerar Dynamic Media är följande ämnen av intresse:

* [Konfigurera Dynamic Media](config-dm.md)
* [Hantera bildförinställningar](managing-image-presets.md)
* [Hantera visningsförinställningar](managing-viewer-presets.md)
* [Felsöka dynamiska media](troubleshoot-dm.md)

Se även följande avsnitt:

* [Videokodning och videoprofiler](video-profiles.md)
* [Bildprofiler](image-profiles.md)

>[!NOTE]
>
>**Om du uppgraderar:**
>
>* När Adobe [!DNL Experience Manager] har startats och körts aktiveras Dynamic Media automatiskt för alla resurser som du överför (om det inte uttryckligen inaktiverats av systemadministratören). Om du är på en uppgraderad instans av [!DNL Experience Manager] och nybörjare på Dynamic Media, måste du troligtvis bearbeta om dina resurser så att de blir aktiverade för Dynamic Media. Se [Bearbeta resurser igen i en mapp](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).
