---
title: Aktivitetsström på tidslinjen
description: I den här artikeln beskrivs hur du visar aktivitetsloggar för resurser på tidslinjen.
contentOwner: AG
feature: Asset Reports,Asset Management
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 20%

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

Aktivitetsloggarna som ska visas på tidslinjen hämtas från platsen `/var/audit/com.day.cq.dam/content/dam` i CRX, där loggfiler lagras.  Dessutom loggas tidslinjeaktiviteten när nya resurser överförs eller befintliga resurser ändras och checkas in i [!DNL Experience Manager] via [Adobe Asset Link](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) eller [[!DNL Experience Manager] datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en).

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
