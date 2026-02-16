---
title: Konfigurera Dynamic Media
description: Om du vill konfigurera Dynamic Media måste du konfigurera Dynamic Media och hantera bild- och visningsförinställningar.
contentOwner: Rick Brough
feature: Configuration,Viewer Presets,Image Presets,Dynamic Media
role: Admin,User
exl-id: 83b70b17-7ee3-41cb-be90-c92ca161660e
source-git-commit: 8a8f3d7b17d79791a3ebf6b583ffcccfcf214470
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Konfigurera Dynamic Media {#setting-up-dynamic-media}

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


## En DNS-uppdatering krävs för förnyelse av certifikat för dynamiska media {#dns-update-dynamic-media-certificate-renewals}

Om din domän använder en CAA-DNS-post (Certification Authority Authorization) måste du auktorisera DigitalCert för att tillåta fortsatt förnyelse av TLS/SSL-certifikat som används av Dynamic Media-värdnamn.

Lägg till följande CAA-post i domänens rot (apex):

```
<yourdomain> CAA 0 issue "digicert.com"
```

Detta är en engångsändring.

Du kan verifiera om det finns en CAA-post med hjälp av DNS-providerverktygen eller ett [CAA-sökverktyg](https://caatest.co.uk/).

Om det finns en CAA-post och DigiCert inte är auktoriserat misslyckas certifikatförnyelsen när det aktuella certifikatet upphör att gälla, vilket kan orsaka driftstopp för bild- och videomaterial. Om det inte finns någon CAA-post för din domän krävs ingen åtgärd.
