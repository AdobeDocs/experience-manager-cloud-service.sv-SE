---
title: Aktivitetsström på tidslinjen
description: I den här artikeln beskrivs hur du visar aktivitetsloggar för resurser på tidslinjen.
contentOwner: AG
feature: Asset Reports, Asset Management
role: Admin, User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
hide: true
hidefromtoc: true
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 16%

---

# Visa resursåtgärdsloggar i aktivitetsström {#activity-stream-in-timeline}

Den här funktionen visar aktivitetsloggar för resurser på tidslinjen. Om du utför någon av följande resursrelaterade åtgärder i [!DNL Experience Manager Assets] uppdaterar funktionen för aktivitetsström tidslinjen för att återspegla aktiviteten.

Följande åtgärder är loggade i aktivitetsströmmen:

* Skapa
* Ta bort
* Ladda ned (inklusive återgivningar)
* Publicera
* Avpublicera
* Godkänn
* Avvisa
* Flytta

Aktivitetsloggarna som ska visas på tidslinjen hämtas från platsen `/var/audit/com.day.cq.dam/content/dam` i CRX, där loggfiler lagras.  Dessutom loggas tidslinjeaktiviteten när nya resurser överförs eller befintliga resurser ändras och checkas in i [!DNL Experience Manager] via [Adobe Asset Link](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) eller [[!DNL Experience Manager] datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=sv-SE).

>[!NOTE]
>
>Övergående arbetsflöden visas inte på tidslinjen eftersom ingen historikinformation sparas för dessa arbetsflöden.

Om du vill visa aktivitetsströmmen utför du en eller flera av åtgärderna för resursen, markerar resursen och väljer sedan **[!UICONTROL Timeline]** i listan GlobalNav.

<!-- ![timeline-2](assets/timeline-2.png) -->

Tidslinjen visar aktivitetsströmmen för de åtgärder du utför på resurserna.

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>Standardplatsen för logglagring för uppgifterna **[!UICONTROL Publish]** och **[!UICONTROL Unpublish]** är `/var/audit/com.day.cq.replication/content`. För **[!UICONTROL Move]**-uppgifter är standardplatsen `/var/audit/com.day.cq.wcm.core.page`.

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
