---
title: Förhandsgranska resurser innan du använder dem på dina AEM Sites-sidor
description: Med Dynamic Media med OpenAPI-funktioner kan du förhandsgranska material på Adobe Experience Manager (AEM) Sites preview-sidor. Med denna förhandsgranskning kan du och dina intressenter granska och validera uppdateringarna av dina resurser innan du publicerar författarsidorna (med uppdaterade resurser) för offentlig användning.
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="Gäller AEM Assets)."
exl-id: 6f071ca9-0f84-45fc-a6b3-047cca9d5e65
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# Förhandsgranska resurser innan du använder dem på AEM Sites-sidor {#asset-preview-using-Dynamic-Media-with-OpenAPI-capabilities}

Med [!DNL Dynamic Media with OpenAPI capabilities] kan du förhandsgranska resurser som är tillgängliga på [!DNL Adobe Experience Manager (AEM) Sites]-författarsidor innan du gör dem tillgängliga för allmänheten. Förhandsgranskningen av resursen är tillgänglig på webbplatsens författare och förhandsgranskningsnivå.

Om du vill [förhandsgranska resurser på AEM Sites förhandsgranskningssidor](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities) uppdaterar du webbplatsens författarsidor genom att antingen lägga till de resurser som du vill förhandsgranska eller ersätta de befintliga som är tillgängliga på den publicerade webbplatssidan. Publicera de uppdaterade författarsidorna på förhandsgranskningsnivån för att generera en förhandsgransknings-URL.

Dela förhandsgranskningssidan med intressenter för att samla in feedback om den visuella kvaliteten och den sammanhangsberoende justeringen av de uppdaterade resurserna. Förfina resurserna baserat på feedback. Skapa och hantera flera versioner av resursen under granskningscykeln.

När du är klar med resurserna för allmänt bruk kan du uppdatera dem på dina författarsidor och publicera sidorna på publiceringsnivån för allmän åtkomst.

## Innan du börjar{#prerequisites-for-previewing-assets-using-Dynamic-Media-with-OpenAPI-capabilities}

Kontrollera att du har:

* Åtkomst till [!DNL AEM Assets as a Cloud Service].
* Behörighet att redigera egenskapen Status för resurser.
* [Ett [!UICONTROL Preview]-värde har lagts till i metadataegenskapen [!UICONTROL &#x200B; Status] som finns på [!UICONTROL Basic] tab &#x200B;](/help/assets/metadata-assets-view.md#edit-metadata-forms) i metadataformuläret som används i mappen som innehåller de resurser som ska förhandsgranskas.
  ![Lägg till förhandsvisningsalternativ](/help/assets/assets/metedata-form-preview.png)
* Nyckeln som genererar förhandsvisningstoken. [Kontakta Adobe support](https://helpx.adobe.com/in/contact.html) och begär en nyckel.

## Förhandsgranska resurser på sidan för webbplatsförhandsgranskning {#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities}

Du kan förhandsgranska nya resurser eller resurser som redan har godkänts. Godkända resurser visas bara på dina aktiva webbplatser.

Utför följande steg för att ställa in objektets status till förhandsgranskning i [!DNL Assets View] och publicera sedan redigeringssidan för webbplatser på förhandsgranskningsnivån för att generera en förhandsgransknings-URL för sidan:

1. Ange resursstatus till **[!UICONTROL Preview]** genom att utföra följande steg:

   1. I [!DNL Assets View] väljer du **[!UICONTROL Assets]** och navigerar till din mapp.
   1. Välj den resurs som ska förhandsgranskas.
   1. Klicka på **[!UICONTROL Details]**.
   1. I [!UICONTROL Information Panel] anger du **[!UICONTROL Status]** till **[!UICONTROL Preview]** och klickar sedan på **[!UICONTROL Save]**.
      ![Förhandsgranska](/help/assets/assets/preview-boat-at-bay.png)

1. Navigera till webbplatsredigeringssidan. Utför stegen i avsnittet [Åtkomst till fjärrresurser i AEM Page Editor](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) om du vill använda panelen Resursväljare för att välja den resurs som du nyligen ställt in på Förhandsgranska (status).

   >[!NOTE]
   >
   > Resursväljaren visar resurser med den senaste statusuppdateringen inställd på Godkänd eller Förhandsgranska.

1. Publicera sidan på förhandsgranskningsnivån med alternativet **[!UICONTROL Manage Publication]**. Utför stegen i avsnittet [Publicera innehåll till förhandsgranskning](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/previewing-content) för att publicera sidan på förhandsgranskningsnivån. Generera en förhandsgransknings-URL för sidan efter publiceringen. På sidan Förhandsgranska visas resurserna (med de senaste statusuppdateringarna) på sidan Platser.

Dela den här förhandsgransknings-URL:en med intressenter för granskning och feedback. Se till att dina intressenter har tillgång till förhandsgranskningssidan. Mer information om hur du ger åtkomst till förhandsgranskningssidorna finns i [Åtkomst till förhandsgranskningstjänsten](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments#access-preview-service).

>[!NOTE]
>
>Huvudkomponenten [för bild V3](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/wcm-components/image#version-and-compatibility) har som standard stöd för förhandsgranskningsversioner av resurser. När du väljer en förhandsvisningsversion av en resurs (resurs med förhandsgranskningsstatus) med panelen [Resursväljare](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/asset-selector-upload), återges den automatiskt av Image V3-komponenten i förhandsgranskningsskiktet (en förhandsversion på webbplatsens författarsida).

När du har slutfört resursversionen [publicerar du dina sidor på publiceringsnivån](#publish-your-pages-to-publish-tier) för offentlig användning.

## Publicera dina sidor med godkänt material för allmänheten{#publish-your-pages-to-publish-tier}

När du har slutfört resursversionen för allmänt bruk anger du resursstatusen till **[!UICONTROL Approved]**. Publicera sedan sidorna på publiceringsnivån. Så här publicerar du sidorna:

1. Följ steg 1 i [Förhandsgranska resurser på sidan för webbplatsförhandsgranskning](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities) ovan för att ändra resursstatus till **[!UICONTROL Approved]**.
1. Navigera till webbplatsens författarsida och publicera den på [!DNL Publish tier]. Publicera sidorna genom att köra stegen i avsnittet [Publicera från sidredigeraren](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/sites/authoring/page-editor/publishing#publishing-from-the-page-editor).
Du kan också följa stegen i avsnittet [Publicera sidor från Sites Console](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/publishing-pages#publishing-from-the-sites-console) för att publicera sidan från webbplatsens konsol.

   >[!NOTE]
   >
   > Endast godkända resurser kan levereras på publiceringsnivån. Godkänn resurserna innan du publicerar sidan på publiceringsnivån för allmänt bruk.

   ![Sidan har publicerats](/help/assets/assets/the-page-has-been-publushed.png)
Ett bekräftelsemeddelande **[!UICONTROL The page has been published]** visas när publiceringen är klar. Navigera till den publicerade sidan på publiceringsnivån för att bekräfta att uppdateringarna är aktiva och att innehållet visas som förväntat.
