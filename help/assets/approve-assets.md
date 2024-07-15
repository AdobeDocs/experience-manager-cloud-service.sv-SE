---
title: Godkänn resurser i Experience Manager
description: Lär dig godkänna resurser i  [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---

# Godkänn resurser i [!DNL Experience Manager]

Varumärkesansvariga och marknadsförare har strikt kontroll över varumärkestillgångarna. Det är bara en godkänd och den senaste versionen av resursen som är tillgänglig för användning, vilket garanterar ett enhetligt varumärke i alla kanaler och tillämpningar.

Ni kan godkänna mediefiler i AEM Assets för att effektivisera resurshanteringen och säkerställa en kontrollerad och effektiv process för hantering av mediefiler.

## Innan du börjar {#pre-requisites}

Du måste ha åtkomst till AEM Assets as a Cloud Service och behörighet för att redigera egenskapen **[!UICONTROL Review Status]** för en resurs.

## Konfiguration

Du måste göra en engångsuppdatering av det tillämpliga metadataschemat i administratörsvyn innan du kan godkänna en resurs. Du kan hoppa över den här konfigurationen för Assets-vyn. Följ de här stegen för att konfigurera metadatamatchemat:

1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Schemas]**.
1. Välj det tillämpliga metadataschemat och klicka på **[!UICONTROL Edit]**. <br>**[!UICONTROL Metadata Schema Form Editor]** öppnas med fliken **[!UICONTROL Basic]** markerad.
1. Rulla ned och klicka på **[!UICONTROL Review Status]**.
1. Klicka på fliken **[!UICONTROL Rules]** på den högra panelen.
1. Avmarkera **[!UICONTROL Disable edit]** och klicka på **[!UICONTROL Save]**.
Om du behöver visa egenskapen som fältet **[!UICONTROL Review Status]** är mappat till går du till fliken **[!UICONTROL Settings]** och visar värdet `./jcr:content/metadata/dam:status` i fältet **[!UICONTROL Map to property]**.

>[!NOTE]
>
>Om dina resurser eller mappar har ett annat standardschema måste du uppdatera i det aktuella schemat.

## Godkänn resurser {#approve-assets}

Du kan godkänna resurser i både [!DNL Experience Manager] och [!DNL Experience Manager Assets]. Så här godkänner du resurser i [!DNL Experience Manager]:

1. Markera resursen/resurserna och klicka på **[!UICONTROL Properties]** i den övre rutan.
1. Bläddra nedåt till **[!UICONTROL Review Status]** på fliken **[!UICONTROL Basic]**.
1. Ändra granskningsstatusen till **[!UICONTROL Approved]**.
   ![bild](/help/assets/assets/approve-old-ui.png)
1. Klicka på **[!UICONTROL Save & Close]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   På samma sätt kan du godkänna resurser med hjälp av den [nya Assets-vyn](/help/assets/manage-organize-assets-view.md).

## Godkänn resurser gruppvis {#bulk-approve-assets}

Effektivisera arbetsflödet genom att snabbt godkänna flera resurser samtidigt. Du kan massgodkänna resurser för att snabba upp godkännandeprocessen, spara tid och öka produktiviteten.
<br>Följ de här stegen för att godkänna gruppresurser i [!DNL Experience Manager]:

1. Skapa en mapp i författarmiljön (https://author-pXXX-eYYY.adobeaemcloud.com). Ersätt _XXX_ med ditt program-ID och _YY_ med miljö-ID från Experience Manager.
1. Navigera till **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Klicka på **[!UICONTROL Create]** överst till höger på sidan.
1. Lägg till en profiltitel och klicka på **[!UICONTROL Create]**. Metadataprofilen har skapats.
1. Markera den nya metadataprofilen och klicka på **[!UICONTROL Edit _(e)_]**. <br>Formuläret **[!UICONTROL Edit Metadata Profile]** öppnas med fliken **[!UICONTROL Basic]** markerad.
1. Dra och släpp **[!UICONTROL Single Line Text Field]** från avsnittet **[!UICONTROL Build Form]** på höger sida till avsnittet Metadata i formuläret.
1. Klicka på det nya fältet och gör sedan följande uppdateringar på panelen **[!UICONTROL Settings]**:
   1. Ändra **[!UICONTROL Field Label]** till _Godkänd Assets_.
   1. Uppdatera **[!UICONTROL Map to property]** till _./jcr:content/metadata/dam:status_.
   1. Ändra standardvärdet till _godkänt_.

1. Klicka på **[!UICONTROL Save]**.
1. På sidan **[!UICONTROL Metadata Profiles]** väljer du den nya metadataprofilen.
1. Klicka på **[!UICONTROL Apply Metadata Profile to Folder(s)]** i det övre åtgärdsfältet.
1. Markera den eller de mappar som du vill godkänna och klicka på **[!UICONTROL Apply]**.
   <br> Behörigheten för hela mappen är inställd för godkännande och alla resurser som överförs till den här mappen godkänns automatiskt.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Detta tillvägagångssätt godkänner de nya resurserna i mappen. För befintliga resurser i mappen måste du välja och godkänna dem manuellt. <br> Du kan också använda alternativet **[!UICONTROL Reprocess]** för att tillämpa ändringarna från metadataprofilen på äldre resurser.

På samma sätt kan du gruppgodkänna resurser i en mapp i Assets-vyn:

1. Markera resurserna och klicka på **[!UICONTROL Bulk Metadata Edit]**.

1. Välj **[!UICONTROL Approved]** i fältet **[!UICONTROL Status]** som är tillgängligt i avsnittet [!UICONTROL Properties] i den högra rutan.

1. Klicka på **[!UICONTROL Save]**.

## Kopiera leverans-URL för godkända resurser {#copy-delivery-url-approved-assets}

Leverans-URL:en för alla godkända resurser i databasen är tillgänglig om du har [!UICONTROL Dynamic Media with OpenAPI capabilities] aktiverat på din AEM as a Cloud Service-instans.

Så här kopierar du en leverans-URL för en godkänd resurs i databasen:

1. Markera resursen och klicka på **[!UICONTROL Details]**.

1. Klicka på ikonen Återgivningar i den högra rutan.

1. Välj **[!UICONTROL Dynamic Media with OpenAPI]** i avsnittet **[!UICONTROL Dynamic]**.

1. Klicka på **[!UICONTROL Copy URL]** för att kopiera resursens leverans-URL.
   ![URL för kopieringsleverans](/help/assets/assets/copy-delivery-url.png)

   >[!NOTE]
   >
   >Alternativet att kopiera leverans-URL för godkända mediefiler är bara tillgängligt i Assets-vyn.

