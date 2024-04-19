---
title: Godkänn resurser i Experience Manager
description: Lär dig hur du godkänner resurser i [!DNL Experience Manager].
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Godkänn resurser i [!DNL Experience Manager]

Varumärkesansvariga och marknadsförare har strikt kontroll över varumärkestillgångarna. Det är bara en godkänd och den senaste versionen av resursen som är tillgänglig för användning, vilket garanterar ett enhetligt varumärke i alla kanaler och tillämpningar.

Ni kan godkänna mediefiler i AEM Assets för att effektivisera resurshanteringen och säkerställa en kontrollerad och effektiv process för hantering av mediefiler.

## Innan du börjar {#pre-requisites}

Du måste ha tillgång till AEM Assets as a Cloud Service och behörighet att redigera **[!UICONTROL Review Status]** egenskap för en tillgång.

## Konfiguration

Du måste göra en engångsuppdatering av det tillämpliga metadataschemat i [!DNL Experience Manager] innan du kan godkänna en resurs. Du kan hoppa över den här konfigurationen för [!DNL Experience Manager Assets]. Följ de här stegen för att konfigurera metadatamatchemat:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.
1. Välj tillämpligt metadatamatchema och klicka på **[!UICONTROL Edit]**. <br>The **[!UICONTROL Metadata Schema Form Editor]** öppnas med **[!UICONTROL Basic]** markerad flik.
1. Rulla ned och klicka **[!UICONTROL Review Status]**.
1. Klicka på **[!UICONTROL Rules]** på den högra panelen.
1. Avmarkera **[!UICONTROL Disable edit]** och klicka **[!UICONTROL Save]**.

>[!NOTE]
>
>Om dina resurser eller mappar har ett annat standardschema måste du uppdatera i det aktuella schemat.

## Godkänn resurser {#approve-assets}

Du kan godkänna resurser i båda [!DNL Experience Manager] och [!DNL Experience Manager Assets]. Godkänna resurser i [!DNL Experience Manager]gör du så här:

1. Markera resursen/resurserna och klicka på **[!UICONTROL Properties]** i den övre rutan.
1. I **[!UICONTROL Basic]** flik, rulla ned till **[!UICONTROL Review Status]**.
1. Ändra granskningsstatus till **[!UICONTROL Approved]**.
   ![bild](/help/assets/assets/approve-old-ui.png)
1. Klicka på **[!UICONTROL Save & Close]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   På samma sätt kan du godkänna resurser med [ny resursvy](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/manage-organize.html?lang=en#manage-asset-status).

## Godkänn resurser gruppvis {#bulk-approve-assets}

Effektivisera arbetsflödet genom att snabbt godkänna flera resurser samtidigt. Du kan massgodkänna resurser för att snabba upp godkännandeprocessen, spara tid och öka produktiviteten.
<br>Följ de här stegen för att godkänna gruppresurser i [!DNL Experience Manager]:

1. Skapa en mapp i författarmiljön (https://author-pXXX-eYYY.adobeaemcloud.com). Ersätt _XXX_ med ditt program-ID och _YYY_ med miljö-ID:t från Experience Manager.
1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Klicka **[!UICONTROL Create]** längst upp till höger på sidan.
1. Lägg till en profiltitel och klicka på **[!UICONTROL Create]**. Metadataprofilen har skapats.
1. Markera den nya metadataprofilen och klicka på **[!UICONTROL Edit _(e)_]**. <br>The **[!UICONTROL Edit Metadata Profile]** formuläret öppnas med **[!UICONTROL Basic]** markerad flik.
1. Dra och släpp en **[!UICONTROL Single Line Text Field]** från **[!UICONTROL Build Form]** -avsnittet på höger sida till avsnittet Metadata i formuläret.
1. Klicka på det nya fältet och gör sedan följande uppdateringar i **[!UICONTROL Settings]** panel:
   1. Ändra **[!UICONTROL Field Label]** till _Godkända resurser_.
   1. Uppdatera **[!UICONTROL Map to property]** till _./jcr:content/metadata/dam:status_.
   1. Ändra standardvärdet till _godkänd_.

1. Klicka på **[!UICONTROL Save]**.
1. I **[!UICONTROL Metadata Profiles]** väljer du den nya metadataprofilen.
1. Klicka **[!UICONTROL Apply Metadata Profile to Folder(s)]** i det övre åtgärdsfältet.
1. Markera mappen/mapparna som du vill godkänna och klicka på **[!UICONTROL Apply]**.
   <br> Behörigheten för hela mappen ställs in för godkännande och alla resurser som överförs till den här mappen godkänns automatiskt.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Detta tillvägagångssätt godkänner de nya resurserna i mappen. För befintliga resurser i mappen måste du välja och godkänna dem manuellt. <br> Du kan också använda **[!UICONTROL Reprocess]** om du vill använda ändringarna från metadataprofilen på äldre resurser.
